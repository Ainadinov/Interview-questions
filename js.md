# 1. Типы данных в CSS?

    -- String
    -- Number 
    -- BigInt
    -- Boolean
    -- Symbol
    -- Object
    -- Null
    -- Underfined

# 2. Разница между == и === ?

    -- == просто сравнивает значение ( 1 == "1" true)
    -- === сравнивает их типы ( 1 === "1" false)

# 3. Разница между FD и FE?

`Function Declaration` - это функция которое создан основном потоке документа,  можно вызывать его до объевление `Hosting` - Сплытие
    fucntion sum(a,b){
        return a + b
    }

`Function Expression` - это созданная функция присвается к переменну
    const expresFunc = fucntion (a,b){
        return a + b
    }