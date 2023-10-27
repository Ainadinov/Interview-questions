# 1. Что такое React?

`React` - JavaScript-библиотека, создано компании Facebook  для создание SPA, Web приложении.

# 2. Что такое JSX?

`JSX` - это расширение JavaScript, которое позволяет добавлять синтаксис XML в JavaScript, отсюда и название JavaScript XML — JSX.  

# 3. Что такое VirtualDOM?

Виртуальная DOM является представлением реальной DOM в памяти. React создает кэш структуры данных в памяти, вычисляет результирующие различия и затем эффективно обновляет отображаемую DOM браузера. Это позволяет программисту писать код, как будто вся страница отображается при каждом изменении, в то время как библиотеки React отображают только те подкомпоненты, которые действительно изменяются.

# 4. Как работает React?

React создает виртуальный DOM. Когда состояние компонента изменяется, он сначала запускает алгоритм сравнения, который идентифицирует, что изменилось в виртуальном DOM. Второй шаг — согласование (reconciliation), при котором DOM обновляется результатами из сравнения.

# 10. Что такое UseCallback ?

`useCallback` - вернеть нам мемеозированный версию callBack.
`Мемеозиование` -перед вызовом функции проверятся, вызывлось ли ранее
                * если не вызвалось то функция вызывается и сохр результат
                * если вызывалось, то исользуется сохраненный результат и не рендерется компонент

```javascript
function App(){
    const [slide, setSlide] = useState(0);

    const getSomeImages = useCallback(()=>{
        return[
            "https/"
        ]
    },[slide])
    // Передаем зависимые данные для отслеживание функции

    function changeSlide(i){
        setSlide(slide => slide + i)
    }

    return(
        <Slide getSomeImages={getSomeImages}/>
        // Функция будеть работать только в дочерном элементе, прямое вызывание функции в компоненте не работает

        <button onClick={()=> changeSlide(1)}>+</button>
    )
}

const Slide = ({getSomeImages}) => {
    const [images, setImages] = useState([]);

    useEffect(()=>{
        setImages(getSomeImages())
    },[getSomeImages])
    // В дочерном элементе функиця вызывается с помощью useEffect по мере нужды вызыва

    return(
        <>
            {images.map((url, i)=> <img key={i} src={url} alt="slide"/>)}
        </>
    )
}

```

# 11. Что такое useMemo?

`useMemo` - вернеть нам мемеозированные значение, закишироваем значение и во время рендеринга компонента значения будеть рендериться если изменен значения переданное в массиве зависимости

```javascript

function App(){
    const [slide, setSlide] = useState(0);

    const countTotal = (num) =>{
        return num + 10
    }

    function changeSlide(i){
        setSlide(slide => slide + i)
    }
    const total = useMemo(()=>{
        return CountTotal(slide);
    },[slide])

    return(
        <div>{total}</div>

        <button onClick={()=> changeSlide(1)}>+</button>
    )
}

```

# 12. Что такое useRef?

`useRef` - ссылка на готовые элементы или компоненты в DOM структуре в функциональным компоненте
        ** прямое обрашение DOM узлу (вместе querySelector, querySelectorAll)
        ** позволяет сохранить какое-то значение и не вызывает перерендеринг

```javascript

function App(){
    const firstRef = useRef();

    useEffect(()=>{
        console.log(firstRef.current)
    },[])

    return(
        <input >{firstRef}</input>
    )
}
```

# 12. Что такое React-Router?

`React-Router` - библеотека который предназначен для маршрутизации в веб-приложениях. 

```javascript
    
import App from './App';
import { BrowserRouter } from 'react-router-dom';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>
);

// Router — это компонент верхнего уровня с отслеживанием состояния, который заставляет работать все остальные компоненты навигации и хуки. В React Router есть BrowserRouter, HashRouter, StaticRouter, NativeRouter и MemoryRouter. Для веб-приложений обычно используется BrowserRouter. Приложение должно иметь один <BrowserRouter>, который обертывает один или несколько <Routes>.

import { Route, Routes } from 'react-router-dom';
import CoffeeHouse from './components/coffee-house/coffee-house';
import OurCoffee from './components/our-coffee/our-coffee';
import SingleCoffee from './components/single-coffee/single-coffee';

function App() {
  return (
    <>
      <SideBar/>
      <div>
        <Routes>
          <Route path="/" element={<CoffeeHouse/>}/>
          <Route path="our-house/" element={<OurCoffee/>}/>
          <Route path="our-house/:i" element={<SingleCoffee/>}/>
        </Routes>
      </div>
    </>
  );
}
// <Routes> проверяет все свои дочерние элементы <Route>, чтобы найти наилучшее соответствие, и отображает эту часть пользовательского интерфейса.

function SideBar(){
    const collections = [
                {
                    category:3,
                    name: "Solimo Coffee Beans 2 kg",
                    country: "Columbia",
                    price: "10.73$"
                },
                {
                    category:3,
                    name: "Solimo Coffee Beans 2 kg",
                    country: "Columbia",
                    price: "10.73$"
                },
            ]

    return(
        <div className="sidebar">
            <Link className="sidebar__link" to="/">Coffee House</Link>
            <Link className="sidebar__link" to="/our-house">Our Coffee</Link>
               
               {collections.map((e,i)=>  
                    <Link  to={"/our-house/" + i} >
                        <div className="coffee__column" key={i}>
                            <img src={CoffeeImg} alt="#"></img>
                            <div className="coffee__name">{e.name}</div>
                            <div className="coffee__country">{e.country}</div>
                            <div className="coffee__price">{e.price}</div>
                        </div>  
                    </Link>)
                }
        </div>
    )
}
// <Link> отображает доступный элемент <a> с реальным href, указывающим на ресурс, на который он ссылается. Клик по ссылке устанавливает URL-адрес и отслеживает историю просмотров.

```