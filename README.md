# 属性进阶-面向对象
## 万物皆属性
    function Product(){
        this.name=''
        this.add=function(){

        }
    }

    Product.prototype={

    }
## 万物皆变量 - 一切数据都是通过变量来统一管理的
    var Product = function(){
        this.name='iphone'
        this.add=function(){}
    }


    Product.prototype={
        buy:function(){

        }
    }
## 属性的取值器和设置器 get set
            Object.defineProperty(this,"price",{
                get:function(){return price*.6},
                set:function( value ){
                    if ( value > 500 ) {
                        console.log("价格太高请核实");
                    }else{
                        price = value;
                    }
                }
            });
           
- 通过get设置的值，使用对象的人员传进去的值都会是6折
- 通过set判断，如果传进去的值大于500，就会在控制台输出。
## 包装器
        //添加一个属性包装器
        Object.defineProperty(this, "produceDate", {
            get: function () {
                // return produceDate.toLocaleDateString();
                return produceDate.toLocaleString();
            },
            set: function (value) {
                produceDate = value;
            }
        });
- 更改时间
- toLocaleDateString() 此函数会转换成本地年月日 生产日期：2017/4/11
- toLocaleString() 此函数会转换成本地年月日+时间 生产日期：2017/4/11 下午5:27:42
## 拓展
    function dateFormat(date,format) {
        var o = {
            "M+" : date.getMonth()+1, //month
            "d+" : date.getDate(),    //day
            "h+" : date.getHours(),   //hour
            "m+" : date.getMinutes(), //minute
            "s+" : date.getSeconds(), //second
            "q+" : Math.floor((date.getMonth()+3)/3),  //quarter
            "S" : date.getMilliseconds() //millisecond
        }
        if(/(y+)/.test(format)) format=format.replace(RegExp.$1,
                (date.getFullYear()+"").substr(4- RegExp.$1.length));
        for(var k in o)if(new RegExp("("+ k +")").test(format))
            format = format.replace(RegExp.$1,
                    RegExp.$1.length==1? o[k] :
                            ("00"+ o[k]).substr((""+ o[k]).length));
        return format;
    }

    //产品对象
    /*对象内如何使用对象的属性和方法：this，对象外如何使用：先实例化，后用点语法*/
    /*类 -- 抽象对象*/
    function Product(name,price) {
        /*属性 行为 可以为空或者给默认值*/
        this.name=name
        this.price=0;
        this.description = '';
        this.zhekou = ''
        this.sales = ''
        this.produceDate
        /*我们的需求：自动计算打折后的价格*/
        Object.defineProperty(this, "price", {
            get: function () {return price*0.9;},
            set: function (value) {
                /*大概普通产品的价格都在0--1万*/
                if(value>10000)
                {
                    alert('产品价格必须在0--1万之间');
                }else{
                    price = value;
                }
            }
        });
        Object.defineProperty(this, "produceDate", {
            get: function () {
                return dateFormat(produceDate,'yyyy-MM-dd');
            },
            set: function (value) {
                produceDate = value;
            }
        });
    }
### 封装一个自己的日期函数
## 兼容性
- 因为这是ECMAScript 5新增特性。所以老版本浏览器不一定支持

- 如果不考虑兼容低端浏览器，可以使用
- 支持浏览器：Chrome 32、IE 9、FireFox 28、Opera 19、Safari 5.1.7
         
