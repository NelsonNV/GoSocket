
# Iniciar proyecto

```bash
go mod init GoSocket

```

## Driver necesarios

- framework gin
- framewrok websocket

```bash
go get github.com/gorilla/websocket
go get github.com/gin-gonic/gin
```

# Cosas de go

### privado y publico

algo importante en go es que en lugar de usar palabras claves como public o private,
se basa en el inicio del nombre de la `func` o el `type`

*si es en mayuscula es public*

```go
type Trade struct {}
```

*si es en minuscula es privado

```go
type trade struct {}
```

lo mismo seria con los atributos en una estructura


## Como cambiar nombre para el json

Al definir el atributo puedo decirse que en json como se llamara el atributo,
ya que digamos en este ejemplo si quiero tener el Symbol en minuscula,
me daria un problema de que seria privado

```go

type Trade struct {
	Symbol    string `json:"symbol"`
	TradeID   string `json:"tradeID"`
	Price     string `json:"price"`
	Size      string `json:"size"`
	Side      string `json:"side"`
	TimeStamp int64  `json:"timestamp"`
}
```

> [!WARNING]
> no debe tener ningun espacio

```go
// mala sintaxy
	Symbol string `json: "symbol"`
// buena sintaxy
	Symbol string `json:"symbol"`
```

## que solo una red pueda entrar

```go
// necesita "github.com/gorilla/websocket"

var upgrader = websocket.Upgrader{
	CheckOrigin: func(r *http.Request) bool {
		return r.Host == "localhost:3000"
	},
}
```

## Diferencia al crear variables

- `var` es una variable grobal
- `:=` es una variable local

## Problemas con los rand

los random necesitan una semilla pero por esa semilla siempre generara el mismo patron si vuelve a usarse

### forma de tener un random mas aleatorio

usando rand de math podemos generar con time una formula que por el tiempo genere un seed mas aleatorio

```go
import (
	"math/rand"
  "time"
  )


	rnd = rand.New(rand.NewSource(time.Now().UnixNano()))

```

## Transformar int a string

Para convertir un entero a una cadena en Go, debes usar el paquete `strconv`, que proporciona las herramientas necesarias para realizar esta conversión.

- Para enteros: `strconv.Itoa`

## Formato de Números Flotantes

Para formatear un número flotante en Go, puedes utilizar la función `strconv.FormatFloat`. Aquí tienes un ejemplo de cómo hacerlo:

```go
strconv.FormatFloat(lastPrice, 'f', 2, 64)
```

- `lastPrice` es la variable que contiene el valor flotante que deseas formatear.
- `'f'` indica que el número debe ser formateado como un decimal estándar.
- `2` especifica el número de decimales que deseas mostrar.
- `64` indica que el número es un flotante de 64 bits.

Esta función es útil para convertir números flotantes a cadenas de texto con un formato específico.

# Cosas de Go

Go trabaja bajo el paradigma de programación asertiva. Cada petición o método tiene dos posibles resultados:

el valor esperado y un error. Si queremos ignorar algun valor, podemos usar el carácter `_`.

# Linkicografía

![Web Sockets Con GO y Pionex](https://www.youtube.com/watch?v=p0IQkI-JkTc)


