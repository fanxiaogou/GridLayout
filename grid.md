# 一. 概念
**我们经常看见的Flexbox布局，table,float,position是一维布局,而css Grid 是二维布局。

简单点就是：  

- 一维布局是只能沿着坐标系统的一个方向进行布局，比如Flexbox的布局，可以通过flex-direction属性来控制沿着x轴布局还是沿着y轴布局  
- 而二维布局是沿着X轴和Y轴一起来布局。**

##一维布局图
![](https://www.w3cplus.com/sites/default/files/blogs/2018/1811/flex-vs-grid-2.png)

##二维布局图
![](https://www.w3cplus.com/sites/default/files/blogs/2018/1811/flex-vs-grid-3.png)  




# 二.重要术语
1. 网格容器(Grid Container)  和网格项(Grid Item) 
   
  	我们使用 display: grid 的元素，container 就是 网格容器(Grid Container)，item 元素就是网格项(Grid Item)。   

		`<div class="container">`   
			`<div class="item item-1"><div>`
  			`<div class="item item-2"></div>`
  			`<div class="item item-3"></div>`
		</div>  `


2.  网格线(Grid Line)  
    网格线是用来在水平和垂直方向分割网格的线,水平方向的网格线是从左向右；垂直方向是从上往下.  

	看下图：我们使用的是3*2的网格线  
	分析：红色的网格线将网格分成三列，蓝色的网格线将网格分成2列
![](https://www.w3cplus.com/sites/default/files/blogs/2016/1609/example-grid-lines-2.png)

3. 网格轨道(Grid Track)  
	两条相邻网格线之间的空间。你可以把它们想象成网格的列或行。下图是第二条和第三条 行网格线 之间的 网格轨道(Grid Track)
![](https://newimg88.b0.upaiyun.com/newimg88/2018/12/terms-grid-track.svg)

4. 网格区域(Grid Area) 
    4条网格线包围的总空间。一个 网格区域(Grid Area) 可以由任意数量的 网格单元格(Grid Cell) 组成。下图是 行网格线1和3，以及列网格线1和3 之间的网格区域。

![](https://newimg88.b0.upaiyun.com/newimg88/2018/12/terms-grid-area.svg)  

5.网格单元格(Grid Cell) 
  两个相邻的行和两个相邻的列网格线之间的空间  
![](https://newimg88.b0.upaiyun.com/newimg88/2018/12/terms-grid-cell.svg)



#三. Grid(网格) 属性目录 #
## 网格容器(Grid Container) 属性 ## 
#### 一. **display**:
将元素定义为网格容器  
值：  
  
1. **grid** ：生成一个块级网格   
2. **inline-grid** ：生成一个内联网格    
  `.container {
  		display: grid | inline-grid;
	}`  

#### 二. **grid-template-columns / grid-template-rows**:  
使用空格分隔的值列表，用来定义网格的列和行  
值：  
1. <track-size>： 可以是长度值，百分比，或者等份网格容器中可用空间（使用 fr 单位）  
2. <line-name>：你可以选择的任意名称  
 
     .container {  
		grid-template-columns: 40px 50px auto 50px 40px;  
  		grid-template-rows: 25% 100px auto;    
	}
![](https://newimg88.b0.upaiyun.com/newimg88/2018/12/template-columns-rows-01.svg)

请注意，一条网格线(Grid Line)可以有多个名称。例如，这里的第二条 行网格线(row grid lines) 将有两个名字：row1-end 和 row2-start ：

	.container {
  		grid-template-rows: [row1-start] 25% [row1-end row2-start] 25% [row2-end];
	}

如果你的定义包含多个重复值，则可以使用 repeat() 表示法来简化定义：

	.container {
  		grid-template-columns: repeat(3, 100px [col-start]);
	}

也可以写成   
	
	.container {
		grid-template-columns: 100px [col-start] 100px [col-start] 100px [col-start];
	}
	.container {
		grid-template-columns: 100px  100px  100px;
	}

特殊单元：fr单元  将网格容器中的自由空间设置为一个份数：  
   		比如：每个网格项设置为网格容器宽度的三分之一

	.container {
	  grid-template-columns: 1fr 1fr 1fr;
	}

	.container {
	  grid-template-columns: repeat(3,1fr);
	}
	
在看例子：
	可用空间总量-200px,再将剩余空间三等分
	.container {
	  grid-template-columns: 1fr 200px 1fr 1fr;
	}
	

#### 三. **grid-template-areas**: 
通过引用 grid-area 属性指定的 网格区域(Grid Area) 名称来定义网格模板  

<grid-area-name>：由网格项的 grid-area 指定的网格区域名称  
1. .(点号） ：代表一个空的网格单元  
2. none：不定义网格区域
   
    .item-a {
     grid-area: header;
    }  
    .item-b {
     grid-area: main;
    }   
    .item-c {
     grid-area: sidebar;
    }     
    .item-d {
     grid-area: footer;
    }     
    .container {
    	grid-template-columns: 50px 50px 50px 50px;
    	grid-template-rows: auto;
    	grid-template-areas: 
      	"header header header header"
      	"main main . sidebar"
      	"footer footer footer footer";
   	}


![](https://newimg88.b0.upaiyun.com/newimg88/2018/12/dddgrid-template-areas.svg)

	
#### 三. **grid-template**:
用于定义 grid-template-rows ，grid-template-columns ，grid-template-areas 简写属性。
值：

1. none：将所有三个属性设置为其初始值


#### 四.**grid-column-gap / grid-row-gap**
指定网格线(grid lines)的大小。  
简单点就是设置列/行之间间距的宽度  
值：

1. <line-size> ：长度值        
     
        .container {
  		 	grid-template-columns: 100px 50px 100px;
  			grid-template-rows: 80px auto 80px; 
  			grid-column-gap: 10px;`
  			grid-row-gap: 15px;`  
         }

![](https://newimg88.b0.upaiyun.com/newimg88/2018/12/dddgrid-gap.svg)   

#### 五.**grid-gap**

设置grid-column-gap 和 grid-row-gap 的简写语法  
   
     .container {
      grid-template-columns: 100px 50px 100px;
      grid-template-rows: 80px auto 80px; 
      grid-gap: 15px 10px; 
     }  

如果grid-row-gap没有定义，那么就会被设置为等同于 grid-column-gap 的值。例如下面的代码是等价的：   

     .container{
 
      /* 等价于 */  
      grid-gap: 10px 10px;
 
      /* 等价于 */  
      grid-gap: 10px;
      }

#### 六.**justify-items**  
沿着 inline（行）轴线对齐网格项(grid items)  
值：  

1. start：将网格项对齐到其单元格的左侧起始边缘（左侧对齐）  
2. end：将网格项对齐到其单元格的右侧结束边缘（右侧对齐）  
3. center：将网格项对齐到其单元格的水平中间位置（水平居中对齐）   
4. stretch：填满单元格的宽度（默认值）  
    
    	.container {
  			justify-items: start | end | center | stretch;
		}   

![](https://pic4.zhimg.com/80/v2-bcd1b451874438b30356a4f83ccd07db_hd.jpg)
#### 七.**align-items**  
沿着 block（列）轴线对齐网格项(grid items)
值：  

1. start：将网格项对齐到其单元格的顶部起始边缘（顶部对齐）  
2. end：将网格项对齐到其单元格的底部结束边缘（底部对齐）   
3. center：将网格项对齐到其单元格的垂直中间位置（垂直居中对齐）  
4. stretch：填满单元格的高度（默认值）  
    
    	.container {
  			align-items: start | end | center | stretch;
		}   

![](https://pic2.zhimg.com/80/v2-df7e149a111300492eb8e29c09aa3b31_hd.jpg)


#### 八.**place-items**  
place-items 是设置 align-items 和 justify-items 的简写形式
值：  
    
    	.container {
  			place-items: start | end;
		}   

#### 九.**justify-content**  
justify-content如果用像px非弹性单位定义的话，总网格区域大小有可能小于网格容器，这时候你可以设置网格的对齐方式（垂直于列网格线对齐）。
值：
1. start:左对齐  
2. end：右对齐  
3. center：居中对齐  
4. stretch：填充网格容器  
5. space-around：在每个网格子项中间放置均等的空间，在始末两端只有一半大小  
6. space-between：两边对齐，在每个网格子项中间放置均等的空间，在始末两端没有空间  
7. space-evenly：网格间隔相等，包括始末两端   
     
    	.container {
  			 justify-content: start | end | center | stretch | space-around | space-between | space-evenly; 
		} 
![](https://pic2.zhimg.com/80/v2-813a63dcc88e693377a8185c23853bb1_hd.jpg)  

#### 九.**align-content**  
align-content如果用像px非弹性单位定义的话，总网格区域大小有可能小于网格容器，这时候你可以设置网格的对齐方式（垂直于行网格线对齐）。  
值：  
1. start：将网格对齐到 网格容器(grid container) 的顶部起始边缘（顶部对齐）  
2. end：将网格对齐到 网格容器 的底部结束边缘（底部对齐）   
3. center：将网格对齐到 网格容器 的垂直中间位置（垂直居中对齐）
4. stretch：调整 网格项(grid items) 的高度，允许该网格填充满整个 网格容器 的高度 
5. space-around：在每个网格项之间放置一个均匀的空间，上下两端放置一半的空间 
6. space-between：在每个网格项之间放置一个均匀的空间，上下两端没有空间  
7. space-evenly：在每个网格项目之间放置一个均匀的空间，上下两端放置一个均匀的空间   
  
 		.container {
		 	align-content: start | end | center | stretch | space-around | space-between | space-evenly; 
			} 
![](https://pic4.zhimg.com/80/v2-2761aa30809f891b4f61e7b1b3bd2a8f_hd.jpg) 

#### 十.**grid-auto-columns / grid-auto-rows** 
任何自动生成的网格轨道(grid tracks)（又名隐式网格轨道）的大小 

当网格中的网格项多于单元格时，或者当网格项位于显式网格之外时，就会创建隐式轨道 

		.container {
		  grid-template-columns: 60px 60px;
		  grid-template-rows: 90px 90px;
		}
这将生成了一个 2×2 的网格。
![](https://newimg88.b0.upaiyun.com/newimg88/2018/12/grid-auto-columns-rows-01.svg) 

      .item-a {
    	 grid-column: 1 / 2;
     	grid-row: 2 / 3;
     }
		.item-b {
  		grid-column: 5 / 6;
  		grid-row: 2 / 3;
		grid-auto-columns:60px;
	}
![](https://newimg88.b0.upaiyun.com/newimg88/2018/12/grid-auto-columns-rows-02.svg)


#四. 子元素 网格项(Grid Items) 属性 # 
通过引用特定网格线(grid lines) 来确定 网格项(grid item) 在网格内的位置。 grid-column-start / grid-row-start 是网格项开始的网格线，grid-column-end / grid-row-end 是网格项结束的网格线。  

值：

1. <line> ：可以是一个数字引用一个编号的网格线，或者一个名字来引用一个命名的网格线 
2. span <number> ：该网格项将跨越所提供的网格轨道数量 
3. span <name> ：该网格项将跨越到它与提供的名称位置  
4. auto：表示自动放置，自动跨度，默认会扩展一个网格轨道的宽度或者高度
 
		.item {
  			grid-column-start: <number> | <name> | span <number> | span <name> | auto
  			grid-column-end: <number> | <name> | span <number> | span <name> | auto
  			grid-row-start: <number> | <name> | span <number> | span <name> | auto
  			grid-row-end: <number> | <name> | span <number> | span <name> | auto
		}
代码：

		.item-1 {
  			grid-column-start: 2;
  			grid-column-end: five;
  			grid-row-start: row1-start
  			grid-row-end: 3;
		}
![](https://pic1.zhimg.com/80/v2-8ae3a7920e65e5c2a243a37ffa99c38c_hd.jpg)

代码：

		.item-2 {
  			grid-column-start: 2;
  			grid-column-end: five;
  			grid-row-start: row1-start
  			grid-row-end: 3;
		}
![](https://pic3.zhimg.com/80/v2-a9159549db272aa6e7c075b479258056_hd.jpg)