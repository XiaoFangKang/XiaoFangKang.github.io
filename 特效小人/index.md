# canvas特效小人


# 介绍：
本站使用小人特效

# 依赖
`jquery.js`
# 源代码
```javascript
/**
 * 小人
 */
function f2() {
    var S_width;
    var S_height;
    var isTouch = 'ontouchstart' in window, START_EVENT = isTouch ? 'touchstart' : 'mousedown',
        MOVE_EVENT = isTouch ? 'touchmove' : 'mousemove',
        END_EVENT = isTouch ? 'touchend' : 'mouseup';
    var powder = [];
//speed:7
    var man = {
        x: 30,
        y: 110,
        step: 0,
        type: 'teststyle',
        speed: 7,
        armlength: 10,
        leglength: 15,
        head: 8,
        body: 25
    };
    var isspread = false;
    var ispowder = true;
//var teststyle=[{armleft0:-45,armleft1:-20,armright0:45,armright1:20,legleft0:-45,legleft1:-20,legright0:45,legright1:20},{armleft0:-60,armleft1:-30,armright0:30,armright1:5,legleft0:-60,legleft1:-30,legright0:30,legright1:5},{armleft0:-70,armleft1:-50,armright0:60,armright1:70,legleft0:-30,legleft1:-50,legright0:70,legright1:20},{armleft0:-10,armleft1:-80,armright0:90,armright1:40,legleft0:-20,legleft1:-60,legright0:90,legright1:10},{armleft0:-80,armleft1:-60,armright0:80,armright1:50,legleft0:-30,legleft1:-40,legright0:90,legright1:80},{armleft0:-60,armleft1:-70,armright0:90,armright1:10,legleft0:-90,legleft1:-60,legright0:40,legright1:70}];
//不行
    var teststyle = [
        {
            armleft0: -45,
            armleft1: -65,
            armright0: 45,
            armright1: 25,
            legleft0: -45,
            legleft1: -65,
            legright0: 45,
            legright1: 25
        },
        {
            armleft0: -30,
            armleft1: -50,
            armright0: 30,
            armright1: 10,
            legleft0: -30,
            legleft1: -50,
            legright0: 30,
            legright1: 10
        },
        {
            armleft0: -15,
            armleft1: -35,
            armright0: 15,
            armright1: -5,
            legleft0: -15,
            legleft1: -35,
            legright0: 15,
            legright1: -5
        },
        {
            armleft0: 0,
            armleft1: -20,
            armright0: 0,
            armright1: -20,
            legleft0: 0,
            legleft1: -20,
            legright0: 0,
            legright1: -20
        },
        {
            armleft0: 15,
            armleft1: -5,
            armright0: -15,
            armright1: -35,
            legleft0: 15,
            legleft1: -5,
            legright0: -15,
            legright1: -35
        },
        {
            armleft0: 30,
            armleft1: 10,
            armright0: -30,
            armright1: -50,
            legleft0: 30,
            legleft1: 10,
            legright0: -30,
            legright1: -50
        }
    ];
//
    var teststyle1 = [
        {
            armleft0: -30,
            armleft1: 0,
            armright0: 30,
            armright1: 0,
            legleft0: -5,
            legleft1: 0,
            legright0: 5,
            legright1: 0
        },
        {
            armleft0: -30,
            armleft1: 0,
            armright0: 15,
            armright1: 0,
            legleft0: -5,
            legleft1: 0,
            legright0: 45,
            legright1: 0
        },
        {
            armleft0: -35,
            armleft1: 0,
            armright0: 15,
            armright1: 0,
            legleft0: -5,
            legleft1: 0,
            legright0: 72,
            legright1: 0
        },
        {
            armleft0: -35,
            armleft1: 0,
            armright0: 0,
            armright1: 0,
            legleft0: -5,
            legleft1: 0,
            legright0: 97,
            legright1: 81
        },
        {
            armleft0: -40,
            armleft1: 0,
            armright0: -15,
            armright1: 0,
            legleft0: -5,
            legleft1: 0,
            legright0: 111,
            legright1: 108
        },
        {
            armleft0: -40,
            armleft1: 0,
            armright0: -15,
            armright1: 0,
            legleft0: -5,
            legleft1: 0,
            legright0: 135,
            legright1: 135
        },
        {
            armleft0: -35,
            armleft1: 0,
            armright0: 0,
            armright1: 0,
            legleft0: -5,
            legleft1: 0,
            legright0: 97,
            legright1: 81
        },
        {
            armleft0: -30,
            armleft1: 0,
            armright0: 15,
            armright1: 0,
            legleft0: -5,
            legleft1: 0,
            legright0: 45,
            legright1: 0
        },

        {
            armleft0: -30,
            armleft1: 0,
            armright0: 30,
            armright1: 0,
            legleft0: -5,
            legleft1: 0,
            legright0: 5,
            legright1: 0
        },
        {
            armleft0: -51,
            armleft1: -27,
            armright0: 51,
            armright1: 41,
            legleft0: -22,
            legleft1: -18,
            legright0: 22,
            legright1: 18
        },
        {
            armleft0: -72,
            armleft1: -54,
            armright0: 72,
            armright1: 82,
            legleft0: -39,
            legleft1: -36,
            legright0: 39,
            legright1: 36
        },
        {
            armleft0: -93,
            armleft1: -81,
            armright0: 93,
            armright1: 123,
            legleft0: -56,
            legleft1: -54,
            legright0: 56,
            legright1: 54
        },
        {
            armleft0: -114,
            armleft1: -108,
            armright0: -114,
            armright1: 164,
            legleft0: -73,
            legleft1: -72,
            legright0: 73,
            legright1: 72
        },
        {
            armleft0: -135,
            armleft1: -135,
            armright0: 135,
            armright1: 164,
            legleft0: -90,
            legleft1: -90,
            legright0: 90,
            legright1: 90
        },
        {
            armleft0: -135,
            armleft1: -135,
            armright0: 135,
            armright1: 164,
            legleft0: -90,
            legleft1: -90,
            legright0: 90,
            legright1: 90
        },
        {
            armleft0: -135,
            armleft1: -135,
            armright0: 135,
            armright1: 164,
            legleft0: -90,
            legleft1: -90,
            legright0: 90,
            legright1: 90
        },
        {
            armleft0: -114,
            armleft1: -108,
            armright0: -114,
            armright1: 164,
            legleft0: -73,
            legleft1: -72,
            legright0: 73,
            legright1: 72
        },
        {
            armleft0: -72,
            armleft1: -54,
            armright0: 72,
            armright1: 82,
            legleft0: -39,
            legleft1: -36,
            legright0: 39,
            legright1: 36
        }
    ];
//var type={armleft0:-45,armleft1:-20,armright0:45,armright1:20,legleft0:-45,legleft1:-20,legright0:45,legright1:20};
    window.onload = function () {

        //new drawpowder('canvas').point(200,200,"rgba(255,252,255,1)");
        //new drawpowder('canvas').init();
        // S_width=document.getElementById("screen").clientWidth;
        // S_height=document.getElementById("screen").clientHeight;
        // document.getElementById('canvas').height=S_height;
        // document.getElementById('canvas').width=S_width;

        var cvs = document.createElement("canvas");
        S_width = window.innerWidth;
        S_height = window.innerHeight;
        cvs.width = window.innerWidth;
        cvs.height = window.innerHeight;
        cvs.id = "canvas";
        cvs.style.cssText = "\
        position:fixed;\
        top:0px;\
        left:0px;\
        z-index:-1;\
        opacity:1.0;\
        ";
        document.body.appendChild(cvs);

    }

    function clearall() {
        var element = document.getElementById('canvas');
        context = element.getContext('2d');
        context.clearRect(0, 0, S_width, S_height);
    }

    function unpowder() {
        clearall();
        ispowder = false;
    }

    function dopowder() {
        clearall();
        ispowder = true;
    }

    function drawpowder(id) {
        var that = this;
        that.element = document.getElementById(id);
    }

    drawpowder.prototype = {
        init: function (e) {
            var that = this;
            //that.element.addEventListener(START_EVENT, that, false);
            //document.addEventListener(MOVE_EVENT, that, false);
            //that.element.addEventListener(END_EVENT, that, false);
        },
        handleEvent: function (e) {
            var that = this;
            switch (e.type) {
                case START_EVENT:
                    that.touchStart(e);
                    break;
                case MOVE_EVENT:
                    that.touchMove(e);
                    break;
                case END_EVENT:
                    that.touchEnd(e);
                    break;
            }
        },
        getPage: function (e, page) {
            return isTouch ? e.targetTouches[0][page] : e[page];
        },
        destroy: function (e) {
            var that = this;
            that.element.removeEventListener(START_EVENT, that, false);
            document.removeEventListener(MOVE_EVENT, that, false);
            that.element.removeEventListener(END_EVENT, that, false);
        },
        touchStart: function (e) {
            try {
                if (e.touches.length > 1) {
                    // 仅处理一根手指
                    e.stopPropagation();
                    e.preventDefault();
                    return;
                }
            } catch (e) {
            }
            var that = this;
            e.preventDefault();
            e.stopPropagation();
            if (isspread) {
                return;
            }
            isspread = true;
            downplacex = that.getPage(e, 'clientX');
            downplacey = that.getPage(e, 'clientY');
            for (var i = 0; i < 88; i++) {
                var tempangle = Math.floor(Math.random() * 360);
                var tempRadians = tempangle * Math.PI / 180;
                var tempdistance = Math.floor(Math.random() * 60);
                var tempcolor1 = Math.floor(Math.random() * 255);
                var tempcolor2 = Math.floor(Math.random() * 255);
                var tempcolor3 = Math.floor(Math.random() * 255);
                powder[i] = {
                    angle: tempangle,
                    Radians: tempRadians,
                    distance: tempdistance,
                    color1: tempcolor1,
                    color2: tempcolor2,
                    color3: tempcolor3,
                    hyaline: 1
                };
            }
            //alert(powder.length)
            for (var j = 0; j < powder.length; j++) {
                //alert(j)
                var Px = Math.cos(powder[j].Radians) * powder[j].distance + downplacex - 50;
                var Py = Math.sin(powder[j].Radians) * powder[j].distance + downplacey - 50;
                //alert(Py)
                //alert(Px)
                that.point(Px, Py, "rgba(" + powder[j].color1 + "," + powder[j].color2 + "," + powder[j].color3 + "," + powder[j].hyaline + ")");
            }
            that.spread();
        },
        touchMove: function (e) {
            try {
                if (e.touches.length > 1) {
                    // 仅处理一根手指
                    e.stopPropagation();
                    e.preventDefault();
                    return;
                }
            } catch (e) {
            }
            var that = this;
            e.preventDefault();
            e.stopPropagation();
        },
        touchEnd: function (e) {
            try {
                if (e.touches.length > 1) {
                    // 仅处理一根手指 e.stopPropagation();
                    e.preventDefault();
                    return;
                }
            } catch (e) {
            }
            var that = this;
            e.preventDefault();
            e.stopPropagation();
        },
        point: function (x, y, color) {
            var that = this;
            context = that.element.getContext('2d');
            //context.clearRect(0,0,400,400);
            context.save();
            context.beginPath();
            context.arc(x, y, 1, 0, Math.PI * 2, true);
            context.fillStyle = color;
            context.closePath();
            context.fill();
            context.restore();
        },
        spread: function () {
            var that = this;
            var time = 0;
            context = that.element.getContext('2d');
            var spreadtimer = setInterval(function () {
                time++
                if (time >= 100) {
                    clearInterval(spreadtimer);
                    powder = [];
                    if (ispowder) {
                        context.clearRect(0, 0, S_width, S_height);
                    }
                    isspread = false;
                    return;
                }
                if (ispowder) {
                    context.clearRect(0, 0, S_width, S_height);
                }
                for (var j = 0; j < powder.length; j++) {
                    powder[j].distance = powder[j].distance + 1;
                    powder[j].hyaline = powder[j].hyaline - 1 / 100;
                    var Px = Math.cos(powder[j].Radians) * powder[j].distance + downplacex - 50;
                    var Py = Math.sin(powder[j].Radians) * powder[j].distance + downplacey - 50;
                    that.point(Px, Py, "rgba(" + powder[j].color1 + "," + powder[j].color2 + "," + powder[j].color3 + "," + powder[j].hyaline + ")");
                }
            }, 10)
        },
        man: function (x, y, step) {
            var that = this;
            var mantype = eval(man.type)[man.step];
            var manx = x;
            var many = y;
            //tui start point
            var legstart = man.body + man.head;
            //tui
            var legleft0X = RetX(mantype.legleft0, man.leglength);
            var legleft0Y = RetY(mantype.legleft0, man.leglength);
            var legleft1Y = legleft0Y + RetY(mantype.legleft1, man.leglength);
            var legright0X = RetX(mantype.legright0, man.leglength);
            var legright0Y = RetY(mantype.legright0, man.leglength);
            var legright1Y = legright0Y + RetY(mantype.legright1, man.leglength);
            //shoubi
            var armleft0X = RetX(mantype.armleft0, man.leglength);
            var armleft0Y = RetY(mantype.armleft0, man.leglength);
            var armright0X = RetX(mantype.armright0, man.leglength);
            var armright0Y = RetY(mantype.armright0, man.leglength);
            //zhichengtui
            var groundleg = legleft1Y > legright1Y ? "left" : "right";
            if (groundleg == "left") {
                many = y - (man.leglength * 2 - legleft0Y - RetY(mantype.legleft1, man.leglength));
            } else {
                many = y - (man.leglength * 2 - legright0Y - RetY(mantype.legright1, man.leglength));
            }
            context = that.element.getContext('2d');
            context.clearRect(0, 0, S_width, S_height);
            context.save();
            context.beginPath();
            context.arc(manx, S_height - many, man.head, 0, Math.PI * 2, true);
            context.lineWidth = 2;
            context.strokeStyle = "#000";

            context.moveTo(manx, S_height - many + man.head);
            context.lineTo(manx, S_height - many + legstart);
            //腿
            context.lineTo(manx + legleft0X, S_height - many + legstart + legleft0Y);
            context.lineTo(manx + legleft0X + RetX(mantype.legleft1, man.leglength), S_height - many + legstart + legleft1Y);
            context.moveTo(manx, S_height - many + legstart);
            context.lineTo(manx + legright0X, S_height - many + legstart + legright0Y);
            context.lineTo(manx + legright0X + RetX(mantype.legright1, man.leglength), S_height - many + legstart + legright1Y);
            //手臂
            context.moveTo(manx, S_height - many + legstart / 2);
            context.lineTo(manx + armleft0X, S_height - many + legstart / 2 + armleft0Y);
            context.lineTo(manx + armleft0X + RetX(mantype.armleft1, man.armlength), S_height - many + legstart / 2 + armleft0Y + RetY(mantype.armleft1, man.armlength));
            context.moveTo(manx, S_height - many + legstart / 2);
            context.lineTo(manx + armright0X, S_height - many + legstart / 2 + armright0Y);
            context.lineTo(manx + armright0X + RetX(mantype.armright1, man.armlength), S_height - many + legstart / 2 + armright0Y + RetY(mantype.armright1, man.armlength));
            context.stroke();
            context.closePath();
            context.restore();
        },
        manwalk: function () {
            var that = this;
            var tw = setInterval(function () {
                man.x = man.x + man.speed;
                man.step = (man.step + 1) % (eval(man.type).length);
                // 关闭跳舞
                // if (man.x > S_width / 2) {
                //     man.speed = 0;
                //     man.type = "teststyle1";
                // }
                if (man.x + 20 >= S_width) {
                    man.speed = -10;
                }
                if (man.x - 20 < 0) {
                    man.speed = 10;
                }
                that.man(man.x, man.y, man.step);
            }, 100)

            setTimeout(function () {
                man = {
                    x: 30,
                    y: 110,
                    step: 0,
                    type: 'teststyle',
                    speed: 7,
                    armlength: 10,
                    leglength: 15,
                    head: 8,
                    body: 25
                };
            }, 30000);
        }
    }
    setTimeout(function () {
        new drawpowder('canvas').manwalk();
    }, 100);

    function RetX(Angle, length) {
        return Math.sin(Angle * Math.PI / 180) * length;
    }

    function RetY(Angle, length) {
        return Math.cos(Angle * Math.PI / 180) * length;
    }
}

```
# 使用方式：
将代码复制的站中的主`js`中。 类似于 `main.js`

# 讲解：

```javascript
setTimeout(function () {
  new drawpowder('canvas').manwalk();
}, 100); 
```
以上代码是用于启动整体动画。
***
```javascript
var tw = setInterval(function () {
                man.x = man.x + man.speed;
                man.step = (man.step + 1) % (eval(man.type).length);
                // 关闭跳舞
                // if (man.x > S_width / 2) {
                //     man.speed = 0;
                //     man.type = "teststyle1";
                // }
                if (man.x + 20 >= S_width) {
                    man.speed = -10;
                }
                if (man.x - 20 < 0) {
                    man.speed = 10;
                }
                that.man(man.x, man.y, man.step);
            }, 100)
```
以上代码是用于人物的动作。（其中有跳舞的动作，但是不用因为太丑了。）
***
## `map` 是人物的各项属性。
```javascript
   var man = {
        x: 30,                       // 人物X向位置
        y: 110,                      // 人物Y向位置
        step: 0,                     // 人物初始化步
        type: "teststyle",           // 类型，teststyle 走路  teststyle1 跳舞
        speed: 7,                    // 人物初始化移动速度
        armlength: 10,               // 人物手臂长度
        leglength: 15,               // 人物腿长
        head: 8,                     // 人物头部大小
        body: 25                     // 人物主体躯干
    }
```





