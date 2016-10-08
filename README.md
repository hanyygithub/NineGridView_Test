NineGridLayout
--------------

1.简介

  这是一个用于实现像微信朋友圈和微博的类似的九宫格图片展示控件，通过自定义viewgroup实现，使用方便。
  多图根据屏幕适配，单张图片时需要自己指定图片的宽高；

----------


2.使用方法

 引用：

    compile 'com.w4lle.library:NineLayout:1.0.0'

 使用：

 在项目的layout文件中添加如下xml即可加入到布局文件

            <com.w4lle.library.NineGridlayout
                android:layout_marginTop="8dp"
                android:id="@+id/iv_ngrid_layout"
                android:layout_height="wrap_content"
                android:layout_width="match_parent" />

支持 padding 和margin

Java Api :

写好自己的Adapter继承自NineGridAdapter:

    class Adapter extends NineGridAdapter {

        public Adapter(Context context, List list) {
            super(context, list);
        }

        @Override
        public int getCount() {
            return (list == null) ? 0 : list.size();
        }

        @Override
        public String getUrl(int position) {
            return getItem(position) == null ? null : ((Image)getItem(position)).getUrl();
        }

        @Override
        public Object getItem(int position) {
            return (list == null) ? null : list.get(position);
        }

        @Override
        public long getItemId(int position) {
            return position;
        }

        @Override
        public View getView(int i) {
            ImageView iv = new ImageView(context);
            iv.setScaleType(ImageView.ScaleType.CENTER_CROP);
            iv.setBackgroundColor(Color.parseColor("#f5f5f5"));
            Picasso.with(context).load(getUrl(i)).placeholder(new ColorDrawable(Color.parseColor("#f5f5f5"))).into(iv);
            return iv;
        }
    }

代码中使用 :

    adapter = new Adapter(context, image);
    viewHolder.ivMore.setAdapter(adapter);
    viewHolder.ivMore.setOnItemClickListerner(new NineGridlayout.OnItemClickListerner() {
        @Override
        public void onItemClick(View view, int position) {
            //do some thing
            Log.d("onItemClick : " + position);
        }
    });


其余API:

    setsetGap //设置图片间隔
    setDefaultWidth //设置单张图片时的宽度，默认 140 * density
    setDefaultHeight //设置单张图片时的高度,默认 140 * density

----------

3.效果


<img src="https://github.com/w4lle/NineGridView/blob/master/boohee_drag.gif">

----------


4.协议

>  /*
 * Copyright (C) 2015 w4lle
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 * http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

