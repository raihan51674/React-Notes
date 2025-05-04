## React part-2
### 1.Custom Navigation:
```js
//1.custom navigation
//2.Rechart,axios
//3.react Router(3) and Outlet
//4.load Data : Loader and useLoader
const Navigation=[
  {
    name : "Home",
    path :"/",
    id: 1
  },
  {
    name : "About",
    path :"/about",
    id: 2
  },
  {
    name : "Contact",
    path :"/contact",
    id: 3
  },
]
function App() {
  const [open, setClose]=useState(false)
  const links=Navigation.map((route)=>{
    return <li className='mx-5'><a href={route.path}>{route.name}</a></li>
  })
  return (
    <div className='flex justify-between text-center'>
      <div className='flex items-center' onClick={()=>setClose(!open)}>
      {open ? <IoCloseSharp className='md:hidden'></IoCloseSharp> : <IoMdMenu className='md:hidden'></IoMdMenu>}
      <ul className={`md:hidden absolute duration-200 ${open ? "top-8":"-top-100"} left-15 bg-black`}>
        {links}
      </ul>
      <h3 className='ml-3'>My Navbar</h3>
      </div>
       <ul className='md:flex hidden'>
       {
          links
       }
       </ul>
       <button>sign up</button>
    </div>
  )
}
```
### 2.Rechart and Axios data load
#### package colection- vi : https://github.com/brillout/awesome-react-components
```js
const data=axios.get("api url");
```
### 3. React Router :
```js

```
### 4.Data load /Loader
```js
//.1 first way
//Router.jsx add
{path:"user",
loader :()=>fetch("https://jsonplaceholder.typicode.com/users") ,
Component:User},

//use
const User = () => {
  const UserData=useLoaderData()
  console.log(UserData);
  return (
 <h3>
{ UserData.map((data)=> <h2 key={data.id}>{data.name}</h2>}
</h3>)
);
};

//2.second way
//Router.jsx
const FetchPromise = fetch("https://jsonplaceholder.typicode.com/users").then(res=>res.json())
export const router = createBrowserRouter([
  {
{path:"user2",
element:<Suspense fallback={<p>Loading data...</p>}>
 <User2 FetchPromise={FetchPromise} ></User2>
</Suspense>
},
}

//use
const User2 = ({FetchPromise}) => {
  const UserData=use(FetchPromise)
  console.log(UserData);
  return (
    <div>
      <h2>User-2 {UserData.length}</h2>
    </div>
  );

{/* <Suspense fallback={
        <div style={{
          display: "flex",
          justifyContent: "center",
          alignItems: "center",
          height: "100vh"
        }}>
    <p>Loading data...</p>
    </div>}>
</Suspense> */}
```
### 5.Dynamic Route:
```js
//1.Routes.jsx
{path:"user/:Id" , 
loader : ({params})=> fetch(`https://jsonplaceholder.typicode.com/users/${params.Id}`),
Component:UserDetails}

//2.link add show more
<Link to={`/user/${data.id}`}>Show Details</Link>

//3.show data
const UserDetails = () => {
  const Userdata=useLoaderData()
  console.log(Userdata);
  const {name,email,address}=Userdata
  return (
    <div>
      <h1>{name}</h1>
      <h2>{email}</h2>
      <h3>{address.city}</h3>
    </div>
  );
};


```












