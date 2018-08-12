# js-caller--callee
 js中的 caller与callee用法


 caller
 
   函数fun的caller返回调用fun的函数对象，即fun的执行环境，如果fun的执行环境为window则返回null
   function fun(){
      console.log(fun.caller)//这里必须写在fun里面，因为caller只有函数执行过程中才有效
  }
  fun();
  //结果为:null
  
  下面包裹一层

    function a(){
        fun();
        function fun(){
            console.log(fun.caller)//这里必须写在fun里面，因为caller只有函数执行过程中才有效
        }
    }
    a();
    
    结果为: a函数
    

   在包裹一层

    function a(){
        b();
        function b(){
            fun();
            function fun(){
                console.log(fun.caller)//这里必须写在fun里面，因为caller只有函数执行过程中才有效
            }
        }
    }
    a();

   结果为: b函数 


  callee
    这个属性在函数的arguments上面
    
    
    function a (){
        console.log(arguments.callee)
    }
    a();
    //结果为a函数本身


  下面一个经典的阶乘函数

    function sum (num){
        if(num <= 1){
            return 1;
        }else{
            return num * (sum(num - 1))
        }
    }
    console.log(sum(5))
    //结果:5*4*3*2*1=120


    为避免函数名称修改致使函数内部报错,改写成下面

    function sum (num){
        if(num <= 1){
            return 1;
        }else{
            return num * (arguments.callee(num - 1))
        }
    }
    console.log(sum(5))
    //结果:5*4*3*2*1=120


  //callee的另外一种用途

    function a(num1,num2,num3){
        console.log(arguments.length);//实参长度为1
        console.log(arguments.callee.length);//行参长度为3
    }
    a(0); 
 


  
  
