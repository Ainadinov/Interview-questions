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