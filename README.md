vue.js
===

~~~
@全域安裝
npm install -g vue-cli

@router 目錄安裝
npm install -D vue-router

@專案建立
vue init webpack-simple 「專案名稱」

@ .vue 可編輯 sytlus css <style lang="stylus">
npm install -D style stylus-loader

@輸出至 index.html
npm run build

@支援 Include HTML
npm install -D vue-resource
~~~

#### 1. {{n}} 置入資料
~~~
<div id="app">

    <h1>{{title}}</h1>
    <p>{{message}}</p>

</div>

<script>
    var vm = new Vue({
        el: '#app',
        data: {
            title: 'vue.js 第 1 課',
            message: '{{n}} 置入資料'
        }
    })
</script>
~~~

#### 2-1. v-bind:placeholder 表單內容說明
~~~
<div id="app">

    <h1>{{title}}</h1>
    <input type="text" v-bind:placeholder="message">

</div>

<script>
    var vm = new Vue({
        el: '#app',
        data: {
            title: 'vue.js 第 2-1 課',
            message: '表單內容說明'
        }
    })
</script>
~~~

#### 2-2. v-model 表單內容
~~~
<div id="app">

    <h1>{{title}}</h1>
    <input type="text" v-model="message">

    <div>{{$data}}</div>
</div>

<script>
    var vm = new Vue({
        el: '#app',
        data: {
            title: 'vue.js 第 2-2 課',
            message: 'v-model 表單內容'
        }
    })
</script>
~~~

#### 2-3. v-model.trim 排除空白
~~~
<div id="app">

    <h1>{{title}}</h1>
    <input type="text" v-model.trim="message">

    <div>{{$data}}</div>
</div>

<script>
    var vm = new Vue({
        el: '#app',
        data: {
            title: 'vue.js 第 2-3 課',
            message: 'v-model.trim 排除空白'
        }
    })
</script>
~~~

#### 2-4. v-model.lazy 省效能，離開後才更換內容
~~~
<div id="app">

    <h1>{{title}}</h1>

    <!--v-model.lazy 省效能，離開後才更換內容-->
    <input type="text" v-model.lazy="message">

    <div>{{$data}}</div>
</div>

<script>
    var vm = new Vue({
        el: '#app',
        data: {
            title: 'vue.js 第 2-4 課',
            message: 'v-model.lazy 省效能，離開後才更換內容'
        }
    })
</script>
~~~

#### 2-5. 表單結果 字母開頭大寫
~~~
<div id="app">

    <h1>{{title}}</h1>
    <p>{{message}}</p>

    <input type="text" v-model="firstName">
    <span>{{firstName | capitalize}}</span>

    <div>{{$data}}</div>
</div>

<script>
    var vm = new Vue({
        el: '#app',
        data: {
            title: 'vue.js 第 2-5 課',
            message: '表單字母開頭大寫',
            firstName: ''
        },

        // 過濾的 function
        filters: {
            capitalize: function(value) {
                return value.toString().charAt(0).toUpperCase() + value.slice(1);
            }
        }
    })
</script>
~~~

#### 2-6. 表單結果 前(後)綴字
~~~
<div id="app">

    <h1>{{title}}</h1>
    <p>{{message}}</p>

    <input type="text" v-model="firstName">
    <span>{{fullName}}</span>

    <div>{{$data}}</div>
</div>

<script>
    var vm = new Vue({
        el: '#app',
        data: {
            title: 'vue.js 第 2-6 課',
            message: '表單結果 前(後)綴字',
            firstName: 'john'
        },

        // function 判斷呈現
        computed: {
            fullName: function() {
                return 'pre - ' + this.firstName;
            }
        }
    })
</script>
~~~

#### 2-7. 表單結果 空字元不帶入前(後)綴字
~~~
<div id="app">

    <h1>{{title}}</h1>
    <p>{{message}}</p>

    <input type="text" v-model="firstName">
    <span>{{fullName}}</span>

    <div>{{$data}}</div>
</div>

<script>
    var vm = new Vue({
        el: '#app',
        data: {
            title: 'vue.js 第 2-7 課',
            message: '表單結果 空字元不帶入前(後)綴字',
            firstName: 'john'
        },

        // function 判斷呈現
        computed: {
            fullName: function() {
                if(this.firstName !== '') {
                    return 'pre - ' + this.firstName;
                } else {
                    return '';
                }
            }
        }
    })
</script>
~~~

#### 3-1. v-if 判斷開關布林值
~~~
<div id="app">

    <h1 v-if="state">{{title}}</h1>
    <p v-if="state">{{message}}</p>

</div>

<script>
    var vm = new Vue({
        el: '#app',
        data: {
            title: 'vue.js 第 3-1 課',
            message: 'v-if 判斷開關布林值',
            state: true // false
        }
    })
</script>
~~~

#### 3-2. v-if v-else 判斷開關布林值
~~~
<div id="app">

    <div v-if="state">{{title}}</div>
    <div v-else="state">{{message}}</div>

</div>

<script>
    var vm = new Vue({
        el: '#app',
        data: {
            title: 'vue.js 第 3-2 課', //state: true
            message: 'v-if v-else 判斷開關布林值', //state: false
            state: false
        }
    })
</script>
~~~

#### 3-3. v-if .length 判斷開關布林值
~~~
<div id="app">

    <div v-if="state.length">{{title}}</div>
    <div v-if="!state.length">{{message}}</div>

</div>

<script>
    var vm = new Vue({
        el: '#app',
        data: {
            title: 'vue.js 第 3-3 課',
            message: 'v-if .length 判斷開關布林值',
            state: []
        }
    })
</script>
~~~

#### 4-1. v-on:click 切換開關
~~~
<div id="app">

    <h1 v-if="state">{{title}}</h1>
    <p v-if="state">{{message}}</p>
    <button v-on:click="state = !state">toggle</button>
    <!--<button @click="state = !state">toggle</button>-->

</div>

<script>
    var vm = new Vue({
        el: '#app',
        data: {
            title: 'vue.js 第 4-1 課',
            message: 'v-on:click 切換開關',
            state: true
        }
    })
</script>
~~~

#### 4-2. @clic 切換開關 Function判斷值
~~~
<div id="app">

    <h1 v-if="state">{{title}}</h1>
    <p v-if="state">{{message}}</p>
    <!--<button v-on:click="toggleState()">toggle</button>-->
    <button @click="toggleState()">toggle</button>

</div>

<script>
    var vm = new Vue({
        el: '#app',
        data: {
            title: 'vue.js 第 4-2 課',
            message: '@clic 切換開關 Function判斷值',
            state: true
        },
        
        // 不須觀察的 function
        methods : {
            toggleState: function () {
                this.state = !this.state
            }
        }
    })
</script>
~~~

#### 5-1. v-for 迴圈列表內容
~~~
<div id="app">

    <h1>{{title}}</h1>
    <p>{{message}}</p>
    
    <ul>
        <li v-for="MyList in List">{{MyList.ch}} {{MyList.name}}</li>
    </ul>

    <hr>

    <ul>
        <li v-for="MyList in List">{{MyList.ch}}</li>
    </ul>

</div>

<script>
    var vm = new Vue({
        el: '#app',
        data: {
            title: 'vue.js 第 5-1 課',
            message: 'v-for 迴圈列表內容',
            List: [{
                name: 'Apple',
                ch: '蘋果'
            }, {
                name: 'Banana',
                ch: '香蕉'
            }]
        }
    })
</script>
~~~

#### 5-2. v-for 帶入計數的迴圈列表內容
~~~
<div id="app">

    <h1>{{title}}</h1>
    <p>{{message}}</p>
    
    <!--index 計數從 0 開始-->
    <ul>
        <li v-for="(MyList, index) in List">{{index + 1}} {{MyList.ch}} {{MyList.name}}</li>
    </ul>

</div>

<script>
    var vm = new Vue({
        el: '#app',
        data: {
            title: 'vue.js 第 5-2 課',
            message: 'v-for 帶入計數的迴圈列表內容',
            List: [{
                name: 'Apple',
                ch: '蘋果'
            }, {
                name: 'Banana',
                ch: '香蕉'
            }]
        }
    })
</script>
~~~

#### 5-3. v-for 迴圈列表只保留第 n 個
~~~
<div id="app">

    <h1>{{title}}</h1>
    <p>{{message}}</p>
    
    <!--index 計數從 0 開始-->
    <ul>
        <li v-for="(MyList, index) in List" v-if="index === 1">{{MyList.ch}} {{MyList.name}}</li>
    </ul>

</div>

<script>
    var vm = new Vue({
        el: '#app',
        data: {
            title: 'vue.js 第 5-3 課',
            message: 'v-for 迴圈列表只保留第 n 個',
            List: [{
                name: 'Apple',
                ch: '蘋果'
            }, {
                name: 'Banana',
                ch: '香蕉'
            }]
        }
    })
</script>
~~~

#### 6. component 置入 HTML template
~~~
<div id="app">

    <h1>{{title}}</h1>
    <p>{{message}}</p>
    
    <list></list>

</div>

<script>

    Vue.component('list',{
        template:`
        <ul>
            <li>蘋果 Apple</li>
            <li>香蕉 Banana</li>
        </ul>
        `
    })

    var vm = new Vue({
        el: '#app',
        data: {
            title: 'vue.js 第 6-1 課',
            message: 'component 置入 HTML template'
        }
    })
</script>
~~~

#### 7. component 置入 HTML template
~~~
<div id="app">

    <h1>{{title}}</h1>
    <p>{{message}}</p>

    <panel :datadata="panelData"></panel>
    <panel :datadata="panelData2"></panel>

</div>

<script>

    Vue.component('panel',{
        template:`
        <div>
            <div v-for="panel in datadata">
                <div>{{panel.title}}</div>
                <div>{{panel.summery}}</div>
            </div>
        </div>`,
        props: ["datadata"]
    })

    var vm = new Vue({
        el: '#app',
        data: {
            title: 'vue.js 第 6-2 課',
            message: 'component 置入 HTML template',
            panelData :[
                {
                    title: 'panelData panel1',
                    summery: 'This is some summery.'
                },
                {
                    title: 'panelData panel2',
                    summery: 'This is some summery.'
                },
                {
                    title: 'panelData pane3',
                    summery: 'This is some summery.'
                }
            ],
            panelData2: [
                {
                    title: 'panelData2 panel1',
                    summery: 'This is some summery.'
                },
                {
                    title: 'panelData2 panel2',
                    summery: 'This is some summery.'
                },
                {
                    title: 'panelData2 pane3',
                    summery: 'This is some summery.'
                }
            ]
        }
    })
</script>
~~~
