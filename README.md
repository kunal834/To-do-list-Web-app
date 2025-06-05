#html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>to-do list</title>
    <link rel="stylesheet" href="style.css">


</head>
<body>
    <div class="container">
        <div class="todoapp">
            <h2> To-do-list <img src="note.png" alt=""></h2>
            <div class="row"> 
                <input type="text" id="inputbox" placeholder="Add your Task ">
                <button onclick="AddTask()"> 
                    ADD
                </button>
            </div>
            <ul id="listcontainer">
             <!-- <li class="checked">Task1</li>
             <li> Task2</li>
             <li>Task3</li> -->

            </ul>
        </div>

    </div>
    <script src="index.js">

    </script>


    
</body>
</html>



#STYLE.CSS
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
.container{
  width : 100%;
  min-height: 100vh;
   background: linear-gradient(135deg , #401394 , #4e085f);
   padding : 10px ; 

}
.todoapp{
    width: 100%;
    max-width: 540px;
    background: #fff;
    margin: 100px auto 20px;
    padding: 40px 30px 70px;
    border-radius: 15px;
}
.todoapp img{
    height: 20px;
}
 .todoapp h2{
    color: #002765;
    display: flex;
    align-self: center;
    margin-bottom: 20px;
    font-weight: bold;
}
.row{
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: #edeef0;
    border-radius: 20px;
    padding-left: 20px;
    margin-bottom: 20px;
}
input{
    flex: 1;    /* it will take the full width above */
    border: none;
    outline: none;
    background: transparent;
    padding: 10px;
    box-shadow: 10px 5px 5px gray;
}

button{
    border: none;
    outline: none ;
    padding : 16px 50px;
    background: #ff5945;
    cursor: pointer;
    border-radius: 40px;
    box-shadow: 10px 5px 5px gray;
}
ul li{
    list-style: none;
    font-size: 18px ;
    padding: 12px 8px 12px 50px ;   
    user-select: none;
    cursor: pointer;
    position: relative;
}
 ul li::before{
    content: '';
    position : absolute;
    height : 28px;
    width: 28px;
    border-radius: 50%;
    background-image: url("unchecked.png");
    background-size: cover;
    background-position: center;
    top: 12px;
    left: 8px;


}
ul li.checked{
    color: #555;
    text-decoration: line-through;
}
ul li.checked::before{
    background-image: url("check_14025690.png");
}
 ul li span{
    position: absolute;
    right: 0;
    top: 5px;
    width: 40px;
    height: 30px;
    font-size: 22px;
    color: #555;
    text-align: center;
    border-radius: 50%;  /* means it is a circle */

}
ul li span:hover{
     background: #bbb5b3;
     }

#INDEX.JS
const inputbox = document.getElementById("inputbox")
const  listcontainer = document.getElementById("listcontainer")
function AddTask(){
    if(inputbox.value === ''){
        alert("you have to write something")
    }
    else{
        let li = document.createElement("li")
        li.innerHTML = inputbox.value;
        listcontainer.appendChild(li); 

        let span = document.createElement("span")
        span.innerHTML = " \u00d7 "
        li.appendChild(span)
    }
    inputbox.value = "";
    savedata();
}

listcontainer.addEventListener("click", function(e){
    if(e.target.tagName  === "LI"){
        e.target.classList.toggle("checked")
        savedata();
    }
    else if( e.target.tagName === "SPAN"){
        e.target.parentElement.remove();
        savedata();


    }

 
},false);

function savedata(){
    localStorage.setItem("data" , listcontainer.innerHTML)
}
function showtask(){
    listcontainer.innerHTML = localStorage.getItem("data"); 
}
showtask()
