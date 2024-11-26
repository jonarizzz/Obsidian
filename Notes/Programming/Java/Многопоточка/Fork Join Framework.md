Был введён в [[Java 7]]

### Суть
- [[{TODO} Рекурсия||Рекурсивное]] разделение большой задачи на подзадачи (Fork)
- Выполнение подзадач (Compute)
- Объединение результатов выполнения (Join)

### Основные классы
1. `ForkJoinPool` — специализированный пул потоков для работы с задачами Fork/Join. Освободившиеся потоки берут новые задачи из очереди задач. При создании желательно явно указать число потоков, иначе займёт все процессоры. 
2. `ForkJoinTask` — базовый класс для задач, которые могут быть декомпозированы.
	1. `RecursiveTask<V>` — для задач, возвращающих результат.
	2. `RecursiveAction` — для задач, которые не возвращают результат.


### Основные методы

- `Compute()` – собственно логика задачи. Абстрактный метод класса `ForkJoinTask` (в `RecursiveTask<V>` возвращает `V`, в `RecursiveAction` возвращает `void`). 
- `Fork()` – отправляет задачу в один из потоков пула. 
- `Join()` – запускает выполнение задачи. 

### Имплементация


``` java
public class ValueSumCounter extends RecursiveTask<Integer> {    
	private int[] array;    
	public ValueSumCounter(int[] array) {        
		this.array = array;    
	}    
	@SneakyThrows    
	@Override    
	protected Integer compute() {        
		if(array.length <= 2) {
			// Если массив достаточно маленький – процессим
			Thread.sleep(1);            
			return Arrays.stream(array).sum();        
		}
		// Если массив большой – делим на два "форка"        
		ValueSumCounter firstHalfArrayValueSumCounter = new ValueSumCounter(Arrays.copyOfRange(array, 0, array.length/2));
		
		ValueSumCounter secondHalfArrayValueSumCounter = new ValueSumCounter(Arrays.copyOfRange(array, array.length/2, array.length));
		
		firstHalfArrayValueSumCounter.fork();
		secondHalfArrayValueSumCounter.fork();
		
		// Объединяем результаты        
		return firstHalfArrayValueSumCounter.join() + secondHalfArrayValueSumCounter.join();    
	}
}

public class Main {    
	public static void main(String[] args) {
		int[] array = getInitArray(10000);
		ValueSumCounter counter = new ValueSumCounter(array);
		System.out.println(new Date());
		ForkJoinPool forkJoinPool = new ForkJoinPool();
		// Запускаем
		System.out.println(forkJoinPool.invoke(counter));
		System.out.println(new Date());    
	}
	
	public static int[] getInitArray(int capacity) {        
		int[] array = new int[capacity];        
		for (int i = 0; i < capacity; i++) {            
			array[i] = 3;        
		}        
		return array;    
	}
}
```

[Понятная статья на Хабре](https://habr.com/ru/articles/565924/)
