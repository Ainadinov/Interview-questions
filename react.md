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

# 16. Что такое useReducer?

`useReducer` - используется когда у вас сложная логика состояние, которая включает себя несколько значений которое изменить один State. Много действий котрое работает одним частью состояние, но по разному его меняет


```javascript

function reducer (state, action){
    switch (action.type){
        case 'increment':
            return {autoplay: state.count + 1};
        case 'decrement':
            return {autoplay: state.count - 1};
        case 'zero':
            return {autoplay: 0};
        default:
            throw new Error();
    }

    // fucntion reducer - пренимает два аргумента
                    //  -- state - начальное значение которое определено в useReducer
                    //  -- action - dispath для передачи type для проверки типов
}

const Slider = () => {
    const [state, dispath] = useReducer(reducer, {count: 0})
    // useReducer - пренимает три аргумента
            // -- function reducer
            // -- начальное состояние, котрое передает в виде объекта
            // -- для линивого создание начального состояние

    return (
        <div>
            <div>{state.count}</div>

            <button onclick={()=> dispath({type: 'increment'})}>toggle autoplay</button>
            <button onclick={()=> dispath({type: 'decrement'})}>toggle autoplay</button>
            <button onclick={()=> dispath({type: 'zero'})}>toggle autoplay</button>

        </div>
    )
}


```

# 16. Что такое HOC?

`HOC` - это один ищ продвинутых способов для повторного использивание логики
    ** функция которое пренимает компонент и возвращает новый компонент
    ** рендерит разную верстку и получает разные данные но логика и строение состояние одинаковые 
    ** использивается для оптимизации и рефакторинга кода


```javascript

import {useState, useEffect} from 'react';

const WithSlider = (BaseComponent, getData)=>{
    return(props)=>{
        const [slide, setSlide] = useState(0);
        const [autoplay, setAutoplay] = useState(false)

        useEffect(() => {
            setSlide(getData());
        }, [])

        function changeSlide(i) {
            setSlide(slide => slide + i);
        }
        return <BaseComponent
                {...props}
                slider={slide}
                autoplay={autoplay}
                ChangesSlide={ChangesSlide}
                SetAutoplay={SetAutoplay}
                />
    }
    // создаем HOC и через аргумент передаем компонент и данные, на выходе получаем зависимости от компонента переданные в аргументе разную верстку и разную данные
}

const getDataFromFirstFetch = () => {return 10};
const getDataFromSecondFetch = () => {return 20};
    // создаем функцию и передаем данные для вызыва HOC

const SliderFirst = (props) => {
    return (
        <>
            <div className="slider w-50 m-auto">
                <div className="text-center mt-5">Active slide {props.slide}</div>
                <div className="buttons mt-3">
                    <button 
                        className="btn btn-primary me-2"
                        onClick={() => props.changeSlide(-1)}>-1</button>
                    <button 
                        className="btn btn-primary me-2"
                        onClick={() => props.changeSlide(1)}>+1</button>
                </div>
            </div>
        </>
    )
}

const SliderSecond = (props) => {
    return (
        <>
            <div className="slider w-50 m-auto">
                <div className="text-center mt-5">Active slide {props.slide} <br/>{props.autoplay ? 'auto' : null} </div>
                <div className="buttons mt-3">
                    <button 
                        className="btn btn-primary me-2"
                        onClick={() => props.changeSlide(-1)}>-1</button>
                    <button 
                        className="btn btn-primary me-2"
                        onClick={() => props.changeSlide(1)}>+1</button>
                    <button 
                        className="btn btn-primary me-2"
                        onClick={() => props.setAutoplay(autoplay => !props.autoplay)}>toggle autoplay</button>
                </div>
            </div>
        </>
    )
}
    // Пустые компоненты без функционала для передачи в HOC качестве арумента, компоненты стали прости, которое просто рендерит кусочек верстки на основани своих пропсов

const SliderWithFirstFetch = withSlider(SliderFirst, getDatafromFirstFetch)
const SliderWithSecondFetch = withSlider(SliderSecind, getDatafromSecindFetch)
    // вызываем HOC

function App() {
    return (
        <>
            <SliderWithFirstFetch/>
            <SliderWithSecondFetch/>
        </>
    );
}

```