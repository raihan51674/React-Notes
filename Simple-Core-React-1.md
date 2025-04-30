## Simple React
### Core Concept part-1
#### 1.Componenet 2.JSX and function name always Capital letter
#### 1.Props (data communication at a components) and only preant to child
```js
function App() {
  return (
    <div>
      <h1>Hello React</h1>
      <Student name="Raihan" dept="cse"></Student>
      <Student name="Rahim" dept="eee"></Student>
    </div>
  );
}
function Student({name,dept}) {
  return (
    <div>
      <h1>Name: {name}</h1>
      <h3>Department: {dept}</h3>
    </div>
  );
}

```
#### 2.Conditional Rendering :(displaying different content based on certain condition or staste )
```js
function App() {
  const time =50;
  return (
    <div>
      <h1>Hello React</h1>
      <Student name="Raihan" dept="cse" done={true}></Student>
      <Todo done={true} task="study completed" time={time}></Todo>
      <TodoVariable done={true} task="study completed"time={time}></TodoVariable>
    </div>
  );
}
function Student({name,dept,done}) {
  return (
    <div>
      {/* conditional rendering ternary */}
      {
        done ? <li>{name}</li> : <li>{dept}</li>
      }
      {/* conditional rendering && (only true return) */}
      {
        done && <h2>{dept}</h2>
      }
      {/* conditional rendering || (only false return) */}
      {
        !done || <h2>{dept}</h2>
      }
    </div>
  );
}
function Todo({done, task,time=0}){ //default use
  if(done === true){
    return <li>Done Task {task} duration{time}</li> //null
  }else{
    return <li>Pendibg {task}</li>
  }
}
//conditional rendering use variable
function TodoVariable({done, task, time}){
  const displyTime = time ? time : "not time"
  let listTask;
  if(done === true){
    listTask = <li>Done Task {task} time show {displyTime}</li> //null
  }else{
  listTask= <li>Pendibg {task}</li>
  }
  return listTask
}

```
### 3.Map Useing Object and array
```js
function App() {
  const friends =["raihan","rifat","mamun","kader"]
  const singer =[
    {id:1, name:"AR Rahman",age:56},
    {id:2, name:"Salma Rahman",age:26},
    {id:3, name:"Arjit sing",age:36}
  ]
  return (
    <div>
      <h1>Hello React</h1>
      <Student friends={friends}  singer={singer}></Student>
    </div>
  );
}
function Student({friends,singer}) {
  return (
    <div>
      {/* //array pass useing map */}
     {
      friends.map((value,index)=>{ //{} use so must return
        return <MyAdda  key={index} value={value}>{value}</MyAdda> 
      })
     } 
     {/* //Object pass using map */}
     {
      singer.map((song)=>{
        return <MyAdda key={song.id} song={song}></MyAdda>
      })
     }
    </div>
  );
}
//show array data
function MyAdda({value,song}){
  return(
    <div>
      {
        value &&  <p>All Friends Name show: {value}</p>
      }
      {
        song && <h1>Singer Details show : {song.name} and {song.age}</h1>
      }
    </div>
  )
}
```
### React Core Concept part -2
#### 1.Event Handle :
```js
const App = () => {
  const handleClick=(e)=>{
   e.preventDefault()
   alert("hello")
  }
  const handleParameter=(para)=>{
    const sum = 3 + para
    alert(sum)
  }
  return (
    <div>
      <h1>Hello React</h1>
      <button onClick={handleClick}>Click me</button>
      {/* just button call fuction */}
      <button onClick={()=> alert("just function")}>Just Function</button>
      {/* parameter given */}
      <button onClick={handleParameter(4)}>Add number</button>
    </div>
  );
};

```
#### 2.State Change (UI chane and remember value after value ) use : dark and light moode,true fasle toggle
```js
const Batmen = () => {
  const [Run, setRun]=useState(0) //value 0,false,"",[],{},null
  const handleClick=()=>{
    const updateCount = Run + 1
    setRun(updateCount)
  }
  const handleSix=()=>{
    const UpdateSix = Run + 6
    setRun(UpdateSix)

  }
  return (
    <div>
      {
        Run > 10 && <p>Oww 10 Run compleated</p>
      }
      <h1>Counter : {Run}</h1>
      <button onClick={handleClick}>Single Run</button>
      <button onClick={handleSix}>Six</button>

    </div>
  );
};

```
#### 3.Data Load and api call using Suspense(loader add)
```js
//First way data loadf
const FetchUser=fetch("https://jsonplaceholder.typicode.com/users").then(res=>res.json());
//Second way data load
const FetchFriends=async()=>{
  const responseData=await fetch("https://jsonplaceholder.typicode.com/users")
  return responseData.json()
}

const App = () => {
  const FriendPromise = FetchFriends()
  return (
    <div>
      <Suspense fallback={<h2>Loading data ...</h2>}>
      <Users FetchUser={FetchUser}></Users>
      </Suspense>
      {/* second way data load */}
      <Suspense fallback={<h2>Friends are coming ...</h2>}>
        <Friends FriendPromise={FriendPromise}></Friends>
      </Suspense>
    </div>
  );
};

function Users({FetchUser}){
  const UsersData=use(FetchUser)
  console.log(UsersData);
  return(
    <div>
     <h2>Show User ALL Data : {UsersData.length}</h2>
    </div>
  )
}
function Friends({FriendPromise}) {
  const FriendsData=use(FriendPromise)
  return(
    <div>
    <h2>Friends Data: {FriendsData.length}</h2>
    {
      FriendsData.map(data=>{
        return <div key={data.id}>
          <h2>{data.name}</h2>
        </div>
      })
    }
    </div>
  ) 
}
```
#### 4.Data Load UseEffect() using
```js
const App = () => {
  const [player, setPlayer]=useState([])

  useEffect(()=>{
    fetch("https://jsonplaceholder.typicode.com/users")
    .then(res=>res.json())
    .then(data=>setPlayer(data))
  },[])
  
  return (
    <div>
      <h3>Players:{player.length} </h3>
    </div>
  );
};

```
