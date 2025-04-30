## React part-2
### 1.Custom Navigation:
```js
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












