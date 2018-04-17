# E-transport
E-Transport是一个基于O2O的同城空闲载荷共享平台，旨在推进同城小、微型物流行业发展，实现城市内部空闲载荷资源利用最大化。本产品自主研发设计，使用界面简洁自然，操作简易，产品与用户互动良好，通过O2O模式能够有效解决同城微、小型货物配送的问题。货主发布货品信息，用户接单，无论用何种交通方式，只需准时安全送达即可。本产品使用户可在货主和运货人两种身份之间切换，合理利用城市的闲散的空闲载荷（以私家车为主），为人们提供便利的同城小、微型运货服务；能有效缓解交通拥堵，缓解城市交通与能源、环境之间的矛盾 <br>

E-Transport is an O2O-based citywide free load sharing platform that aims to promote the development of small and micro-logistics in the same city and maximize the utilization of idle load resources in the city. This product is designed and developed independently, the interface is simple and natural, easy to operate, and the product and user interaction is good, O2O mode can effectively solve the city micro and small cargo distribution problems. The owner of the release of goods information, user orders, no matter what kind of transport, just on time and secure delivery. This product allows users to switch between the two identities of the owner and the consignor, make reasonable use of the city's idle idle load (mainly by private cars), to provide people with convenient small city, micro-delivery services; can effectively ease Traffic congestion, ease the city traffic and energy, environmental conflicts.

## 功能展示
主要有下单，接单，订单管理，个人中心，图片上传等等功能 <br>
![allover1](https://github.com/Ather1995/E-transport/blob/master/display/lsj1.gif?raw=true) <br>
![allover2](https://github.com/Ather1995/E-transport/blob/master/display/lsj2.gif?raw=true) <br>

## 界面
### 1
![logic](https://github.com/Ather1995/E-transport/blob/master/display/mainPage.png?raw=true) 
![logic](https://github.com/Ather1995/E-transport/blob/master/display/logic.png?raw=true) <br>
### 2
![account](https://github.com/Ather1995/E-transport/blob/master/display/account.png?raw=true) 
![acorder](https://github.com/Ather1995/E-transport/blob/master/display/acorder.png?raw=true) <br>
### 3
![commonAddr](https://github.com/Ather1995/E-transport/blob/master/display/commonAddr.png?raw=true) 
![giveorder](https://github.com/Ather1995/E-transport/blob/master/display/giveorder.png?raw=true) <br>
### 4
![login](https://github.com/Ather1995/E-transport/blob/master/display/login.png?raw=true) 
![my](https://github.com/Ather1995/E-transport/blob/master/display/my.png?raw=true) <br>
### 5
![order](https://github.com/Ather1995/E-transport/blob/master/display/order.png?raw=true) <br>

## 技术要点
### 1
对Activity进行了封装，以便实时查看activity的调用过程 <br>
我们自己写了一个类BaseActivity继承于类AppCompatActivity，并且实现了他的onCreate和onDestroy的功能，还在log里面在调用和销毁BaseActivity的时候进行输出，以便更好的对Activity进行管理

### 2
项目中用了四大布局中的三个：LinearLayout、RelativeLayout、FrameLayout <br>
LinearLayout：线性布局是本项目的主要布局,常规页面基本的布局架构都是依赖于线性布局实现的. <br>
RelativeLayout：相对布局主要用在一些需要层次叠放的位置，比如对一些图片的处理使用到了该布局  <br>
FrameLayout：该布局用在了需要实现在同一个Activity需要动态加载不同界面的地方,比如一打开App的三个可切换的页面上  <br>

### 3
异步处理 <br>
通过handler+message的机制，实现异步对页面前端UI的更改。并且实现动态改变轮播图，以及发送短信以后的倒计时功能 <br>
### 4
intent传递对象 <br>
通过实体类实现Serializable接口，完成get和set的函数，对实体类对象进行传递  <br>

### 5
高德Map <br>
定位。整合高德地图服务，通过AMapLocationClient类实现定位，创建AMapLocationClientOption对象设置定位的模式和相关参数, 为连续定位，蓝点不会移动到地图中心点(为方便搜索)；搜索。poi搜索关键字，用一个PoiItem类型list存储取得第一页的poiitem数据，实现关键字检索 POI; 获取搜索点的经纬度，和规范地址(**省**市*区的形式,非POI。将关键字解析GeocodeSearch(),获得经纬度RegeocodeQuery(),再逆解析获得规范地址，存入数据库； <br>
注：1、虚拟机上不支持显示地图，应该是opengl显示不支持，会空对象引用问题(null object reference) <br>
 2、解析，逆解析是以异步方式进行，故要注意异步问题，否则第一次获取的经纬度为空，第一次逆解析失败。 <br>
