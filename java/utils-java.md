# JAVA

## Arraylists

- create : `ArrayList<String> myt = new ArrayList<String>();`
- add : `myt.add(item);`
- get item at index : `myt.get(idx);`
- update item : `myt.set(idx, newItem);`
- remove item : `myt.remove(idx); myt.remove(Object);`
- find Item : `myt.contains(Object); #return true or false`
- get idx of element : `int position = myt.indexOf(searchItem); #return -1 if not exist, else return pos`

## Collection Interface Methods

Some of the methods of Collection interface are:

- Boolean add ( Object obj),
- Boolean addAll ( Collection c),
- void clear(), etc.
  which are implemented by all the subclasses of Collection interface.
- [Binary_Search] = `int foundSeat = Collections.binarySearch(myList, targetEl, null) ;`
- Collections.min(mycoll);
- Collections.max(mycoll);
- Collections.swap(list, idx1, idx2);

## Maps

- `map.put(key,val);` # return null if element not in map.
- `String value = map.get(key);`
- `map.containsKey(key);` # return true if key in map
- remove key-value pair from map:
  - `Sring prevEntry = map.remove(key);`
  - `boolean isRemoved = map.remove(key, value);` #remove only key-value pair if exist.
- Replace entry for a key:

  - `String prevEntry = map.replace(key, new_entry);` #return null if key does not exist.
  - `boolean isReplaced = map.replace(key, prevEntry, newEntry);`

- create unmodifiable map:
  - `Map<String, String> m = Collections.unmodifiableMap(map);`
- loop through map :

```
 for (Map.Entry<String, Integer> me : hm.entrySet()) {
            // Printing keys
            System.out.print(me.getKey() + ":");
            System.out.println(me.getValue());
  }
  #############

  for(String key: hm.keySet()){
    sout(key + hm.get(key));
  }
```

```
Map<String, String> languages = new HashMap<>();
languages.put(key,value);
String val1 = languages.get(key);
```

## JAVA I/O

```
## FileWriter
    FileWriter locFile = null;
    locfile = new FileWriter("locations.txt");
    for (Location location : locations.values()){
      locfile.write(location.getID() + ... + '\n');
    }
    locfile.close();
---- try with resources if class implements closeable
    try (FileWriter locfile = new FileWriter("locations.txt") ) {} //no need to close


## FileReader
  // 1, loc1
  // 2, loc2
  try {
    scanner = new Scanner(new FileReader('location.txt'));
    scanner.useDelimiter(",");
    while(scanner.hasNextLine()){
      int loc = scanner.nextInt();
      scanner.skip(scanner.delimiter());
      String description = scanner.nextLine();
    }
  }catch(IOException e){
    e.printStackTrace();
  }

## BufferedReader Method1
  FileReader reader = new FileReader("geeks.txt");
  BufferedReader buffer = new BufferedReader(reader, 16384);
  while(true){
    String line = buffer.readLine();
  }

## BufferedReader Method2
  try{
    scanner = new Scanner(new Bufferedreader(new FileReader("location.txt"))) ;
    while (scanner.hasNextLine()) {
      String input = scanner;nextLine();
      String[] data = input.split(',');
      int loc = Integer.parseInt(data[0]);
      String direction = data[1];
    }
  }

## BufferedOutputStream (write to file, but not readable format)

    try ( DataOutputStream locFile = new DataOutputStream( new BufferedOutputStream( new FileOutputStream( "file.dat")))) {
      locfile.writeInt(2);
      locFile.writeUTF("str");
    }

## Read Binary DATA
    try ( DataInputStream locFile = new DataInputStream( new BufferedInputStream( new FileInputStream( "file.dat")))) {
      int locId = locFile.readInt();
      String description = locFile.readUTF();
    }

## Serialize Object (Write)
    try ( ObjectOutputStream locFile = new ObjectOutputStream( new BufferedOutputStream( new FileOutputStream( "file.dat")))) {
      locFile.writeObject(myObject);
    }

## Serialize Object (Read)
    try ( ObjectInputStream locFile = new ObjectInputStream( new BufferedInputStream( new FileInputStream( "file.dat")))) {
      Location location = (Location) locFile.readObject();
    }
```

## Threads

- in file 1 create ConcreteThreadClass that extends Thread.
- overrid run method.
- in file 2 create instance of this concrete class.
- use `myThread.start()` to start the thread.

```
# METHOD 1
- extend Thread
Thread myThread = new MyThread();
myThread.setName("name_to_thread");
myThread.start();

- in threadclass call : currentThread().getName();

# METHOD 2
- implement Runnable
- Thread myRunnableThread = new Thread(new myRunnable());
```

- Thread sleep = `Thread.sleep(3000);//exception InterruptedException , use in thread class`
- Interrupt a thread = `myThread.interrupt();`
- Join = `anotherThread.join();`

- commands:

```
myThread.start();
myThread.join(); || myThread.join(time)
myThread.interrupt();
```

## Lambdas

- Loop with lambdas = `list.forEach( () -> { } ); `
- Streams :

```
// using lambda to filter data
        Stream<Product> filtered_data = list.stream().filter(p -> p.price > 20000);

        // using lambda to iterate through collection
        filtered_data.forEach(
                product -> System.out.println(product.name+": "+product.price)
        );
```

## Functional Interfaces

- interface with 1 abstract method, use annotation `@FunctionalInterface`.
- Function :

```
Function<entrée, sortie> getFirstName = (Entrée var) -> {
  return of type sortie ;
};
String firstName = getFirstName.apply(employee.get(0)); //String is type sortie defined in Function.
```

## Streams

```
myCollection
  .stream()
  .map(s-> bbb)
  .filter( s -> startsWith("g"))
  .sorted()
  .forEach(System.out::println);

-------------
Stream<String> ls1 = Stream.of("a","b","c");
Stream<String> ls2 = Stream.of("d","e","f");
Stream<String> concatStream = Stream.concat(ls1,ls2);
concatStream.distinct().count();

-------------
List<String> myList = Stream.of("a", "b")
  .map(String::toUpperCase)
  .collect(Collectors.toList());

products
    .stream()
    .map(productInfo::getQuantity);

------------- FlatMap (used for list of list) vs Map
  List<List<String>> list = Arrays.asList(
    Arrays.asList("a"),
    Arrays.asList("b"));
  System.out.println(list);

  list
    .stream()
    .flatMap(Collection::stream)
    .collect(Collectors.toList())

  departments.stream()
    .flatMap(department -> department.getEmployees().stream())
    .collect(Collectors.toList())

------------ Group By
Map<Integer, List<Employee>>  groupedByAge =
              departments
              .stream()
              .flatMap(deparment -> department.getEmployees().stream())
              .collect(Collectors.groupingBy(employee -> employee.getAge()));

```

## Tests

- use delta parameter for double precision : `assertEquals(expected, account.getBalance(), .01);`.
