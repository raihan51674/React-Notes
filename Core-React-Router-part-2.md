## React part-2
### 1.Custom Navigation:
```js
//1.custom navigation
//2.Rechart,axios
//3.react Router(3) and Outlet
//4.load Data : Loader and useLoader



//Navbar section must be add "w-11/12 mx-auto fixed left-0 right-0 z-50 "
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


//extra styleing
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
### 4.5 Data load  instaln button ar niche show: 1 ta show with loader
```js
//user componenet
const [showInfo, setShowInfo]=useState(false)
const userPromis= fetch(`https://jsonplaceholder.typicode.com/users/${data.id}`).then(res=>res.json())
//return ar por
<button onClick={()=>setShowInfo(!showInfo)}>{showInfo ? "Hide":"Show"}-Info</button>
{
 showInfo && <Suspense fallback={<p>Loadng...</p>}>
<INstalDataLoadDetails userPromis={userPromis}></INstalDataLoadDetails>
</Suspense>
}
//data show
const INstalDataLoadDetails = ({userPromis}) => {
  const {name,username}=use(userPromis)
  return (
    <div>
      <h1>Show ingo {name} and {username}</h1>
    </div>
  );
};
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

//route.jsx ar loader teke params ar id dore je kono componenet a use korte parvo
const {Id}=useParams()
  console.log(Id);
```
### 6.useNavigate / redirect(spacific place where)
```js
//1.useNavigate
const navigate=useNavigate()
<button onClick={()=>navigate("/")}>Dekhao Product</button>
<button onClick={()=>navigate(`/user/${data.id}`)}>Dekhao Product</button>

//previous section
<button onClick={()=>navigate(-1)}>Go Back</button>

//componen akare use
 const [VisitHome,setVisitHome]=useState(false)
if(VisitHome){
   return <Navigate to="/"></Navigate>
  }
//return ar por
 <button onClick={()=>setVisitHome(true)}>Vist Home</button>
```
### 7.Loader add Global 
```js
//Global
const RootLayout = () => {
  const navigation=useNavigation()
  const isNavigating =Boolean(navigation.location)
  return (
    <div>
      <Header></Header>
      {isNavigating && <p>Loading...</p> }
      <Outlet></Outlet>
    </div>
  );
};

```
### 8.Not Found 404 Route
```js
//use paren route
 {
    path:"*",
    element:<h2>Not Found</h2>
  }
```
### 9.useLocation :












