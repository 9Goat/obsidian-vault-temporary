computed properties is a way in vue to return values that change through out the program without having to declare variables inside the return  data function. We use computed when we want to have a variable that dynamically changes it value depending on the other variables that define its value

# Syntax

```Js
// after a method liker return or methods we can create computed
, // <-- important comma for separation
computed:{

functionName(no parameters here){
//statements to execute
return value ; //very important the entire idea of a computed is to return a value
}

}

// calling the method in html like a normal varaible

<p> {{functionName}}</p>;
```

# Example

```Html
<div id="app">
        <p>the value of the variable before the computd: {{variable1}}</p>
        <p>the value of the computed: {{sumOfVariable}}</p>
        <p>the vlaue of the variable after the computed: {{variable1}}</p>
        <h1>showcasing that computed can access and modify variables using this</h2>
        <p>the value of the computed: {{sumOfVariable2}}</p>
        <p>the vlaue of the variable after the computed: {{variable2}}</p>

    </div>
    <script>const app = Vue.createApp({
    data(){
        return{
            variable1 : 10,
            variable2 : 10,
        }
    },
    computed:{
        sumOfVariable(){
            sum = 0;
            temp = this.variable1;
            for (;temp >0;temp--)
                sum += temp;
            return sum;
        },
        sumOfVariable2(){
            sum = 0;
            for (;this.variable2 >0;this.variable2--)
                sum += this.variable2;
            return sum;
        }
    }
})

const mountedApp =  app.mount("#app");</script>
```

# Notes

-  we **CANNOT** pass parameters to a computed property
- to access variables and methods inside of computed we add before them the keyword **this** followed by a point .
	- **Example** : this.variable or this.function()
- we **MUST** return a value when we create a computed
- the computed get called when:
	1. when we first execute the page
	2. every time a change happens to a variable we accessed using **this** inside the computed
- we access computed the same way we access variables by surrounding them with double curly brackets **{{}}**