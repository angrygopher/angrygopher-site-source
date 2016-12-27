+++
comments = true
date = "2016-12-27T18:03:23-02:00"
title = "WaitGroup"
draft = false
toc = false
slug = ""

+++

WaitGroup waits for a certain number of goroutines to be finalized and then continues with execution.

### Example

```go
package main

import (
	"math/rand"
	"sync"
	"time"
)

func routine(wg *sync.WaitGroup, x int) {
	// Wait a random time
	rt := rand.Int31n(1000)
	time.Sleep(time.Duration(rt) * time.Millisecond)

	println("goroutine ", x)
	wg.Done() // Decrements the WaitGroup counter.
}

func main() {

	println("Start")
	rand.Seed(time.Now().Unix())

	//Creates a wait group to wait all goroutines
	var wg sync.WaitGroup

	//Sets the number of goroutines to wait for
	wg.Add(3)

	for i := 1; i < 4; i++ {
		go routine(&wg, i)
	}

	//Hold execution until the WaitGroup counter reaches 0.
	wg.Wait()

	println("End")

}
```

[Test on Playground](https://play.golang.org/p/MmLhsQmlQ4)