# nodejs-async-workshop
This workshop will cover all pattern to manage asynchronocity in nodejs.

We will use a simple exercise as a subject to implement the different pattern to manage asynchronous code.

The exercise is the following : 

We have multiple reader that wants to read different files, to improve our performance we would like to be able to cache the result of a read operation and avoid to do multiple read on the same file.

You must provide a method that create a reader, the reader should allow the following : 
- it should take in parameter a filename
- it should manage reading the file if one exists for the filename
- it should set in a cache the result of the read operation when it has been done
- it should provide a way to be able to execute some code after the read operation has been done
- it should return the content stored in the cache instead of doing a new read operation, if a cache exist for the filename


You will have to implement this for the following pattern in the following order : 

1. Implement using only callback using the `readFile` method from `fs`
2. Implement using only Promise (no async/await), you will promisify the `readFile` method from `fs`
3. Transform the code by using the `readFile` method from `fs/promises`
4. Implement using only async/await using the `readFile` method from `fs/promises`
5. Implement using only EventEmitter, you will decorate the `readFile` method from `fs` to make it send event when data is read
6. Implement using only eventApi and eventEmitter using the `createReadStream` method from `fs`

Example of what could be a process using this method for the first implementation using callback : 

```js
const reader1 = createFileReader('file.json')
reader1.onDataReady(data => {
  console.log(`First time get data : ${data}`)
  
  // do any treatments 
  
  // try to read the same file a second time
  const reader2 = createFileReader('file.json')
  reader2.onDataReady(data => {
    // this time data shall comes from a cache
    console.log(`Second time get data : ${data}`)
  })
})
```
