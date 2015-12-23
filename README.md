# Android L版本中新增了RecyclerView、CardView 、Palette。

### RecyclerView

  RecyclerView作为替代ListView使用，RecyclerView标准化了ViewHolder，ListView中convertView是复用的，在RecyclerView中，是把ViewHolder作为缓存的单位了，然后convertView作为ViewHolder的成员变量保持在ViewHolder中，也就是说，假设没有屏幕显示10个条目，则会创建10个ViewHolder缓存起来，每次复用的是ViewHolder，所以他把getView这个方法变为了onCreateViewHolder。 ViewHolder更适合多种子布局的列表，尤其IM的对话列表。RecyclerView不提供setOnItemClickListener方法，你可以在ViewHolder中添加事件。RecyclerView的使用可以参考《Material Design UI Widgets》。

RecyclerView可以实现横向、纵向滑动视图：

![mahua](https://raw.githubusercontent.com/3332523marco/androidl/master/recyclerview1.png =220x380)                  &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;![mahua](https://raw.githubusercontent.com/3332523marco/androidl/master/recyclerview2.png =220x380)           
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;RecyclerView 1                                                &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;RecyclerView 2

    @Override  
    protected void onCreate(Bundle savedInstanceState) {  
       super.onCreate(savedInstanceState);  
       setContentView(R.layout.activity_recycler_view_horizontal);  
  
       // specify an adapter (see also next example)  
       List<MyAdapter.Item> itemList = new ArrayList<MyAdapter.Item>();  
       for (int i = 0; i < 100; i++)  
           itemList.add(new MyAdapter.Item("Item " + i, "world"));  
       mAdapter = new MyAdapter(itemList);  
  
  
       mRecyclerViewHorizontal = (RecyclerView) findViewById(R.id.my_recycler_view_horizontal);  
       mRecyclerViewHorizontal.setHasFixedSize(true);  
  
       // use a linear layout manager  
       LinearLayoutManager mLayoutManager = new LinearLayoutManager(this);  
       mLayoutManager.setOrientation(LinearLayoutManager.HORIZONTAL);  
       mRecyclerViewHorizontal.setLayoutManager(mLayoutManager);  
       mRecyclerViewHorizontal.setAdapter(mAdapter);  
     }  
     
### CardView
  CardView继承自FrameLayout类，可以在一个卡片布局中一致性的显示内容，卡片可以包含圆角和阴影。CardView是一个Layout，可以布局其他View。CardView 的使用可以参考《Material Design UI Widgets》。文章最后会给出这篇文章示例代码。
  
  ![mahua](https://raw.githubusercontent.com/3332523marco/androidl/master/cardview.png =220x380)                  &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;![mahua](https://raw.githubusercontent.com/3332523marco/androidl/master/palette.png =220x380)           
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;RecyclerView 1                                                &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;RecyclerView 2

### Palette
Palette从图像中提取突出的颜色，这样可以把色值赋给ActionBar、或者其他，可以让界面整个色调统一，效果见上图（Palette）。

Palette这个类中提取以下突出的颜色：

* Vibrant  （有活力）
* Vibrant dark（有活力 暗色）
* Vibrant light（有活力 亮色）
* Muted  （柔和）
* Muted dark（柔和 暗色）
* Muted light（柔和 亮色）

提取色值代码如下：

     Bitmap bm = BitmapFactory.decodeResource(getResources(), item.image);  
          Palette palette = Palette.generate(bm);  
          if (palette.getLightVibrantColor() != null) {  
              name.setBackgroundColor(palette.getLightVibrantColor().getRgb());  
              getSupportActionBar().setBackgroundDrawable(new ColorDrawable(palette.getLightVibrantColor().getRgb()));  
              // getSupportActionBar().  
  
          }  
