# Streams

## **IO (InputOutput)**
- Transfering the data in and out from the resources to program. It is called Input Output.

## **Stream **
- Stream is a **flow of data**. Data may be flow from resouce to program or program to resource. 
    - Just like a water flow from tank to bucket.
- Data will be send in the form of Byte or Chars not a whole chunk. ex: name=John, It will not send as whole string. It will be either send as character like 'J','O','H','N' or in byte. 
- Types of Streams
    - **Byte Stream (1 byte)**
        - InputStream
        - OutputStream
    - **Char Stream (2 byte)**
        - Reader
        - Writer

- What is **buffer**?
    - If the speed of the data send from resource to the Java program environment would not be same, in that case data might get lost. To avoid that, Transfer the data to buffer. Then reciever will get the complete data.
        - Example: While watching videos in mobile buffer initially to load the high quality videos. Because the rate the resource sending the data and rate at which video displayed in video would be different.      
 
 ![IO Stream Flow!](../Images/IO_Streams_ss.png "IO Stream"){ width: 200px; }