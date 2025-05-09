**StackOverflowError** — это [[{TODO} Error||ошибка]] в программировании, возникающая, когда стек вызовов переполняется. Она типична для языков с ограниченным стеком, таких как Java.

### Когда возникает?

Ошибка происходит, когда глубина [[Рекурсия (Recursion)||рекурсивных]] вызовов становится слишком большой, и [[Stack (Область Памяти)||стек]] не может вместить все данные. Это может быть вызвано:

- **Бесконечной рекурсией** – функция вызывает саму себя без выхода. 
	- **Решение**: использовать итерацию и выход из рекурсии.
- **Глубокой рекурсией** – даже если есть выход, но он слишком далёк, стек может закончиться. 
	- **Решение**: использовать итерацию и выход из рекурсии.
- **Большим количеством локальных переменных** – они хранятся в стеке и могут быстро его заполнить. 
	- **Решение:** хранить большие данные в куче (Heap).

  
