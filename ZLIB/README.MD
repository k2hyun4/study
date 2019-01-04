# zlib?
* https://ko.wikipedia.org/wiki/Zlib

# decompression in java
```
  private String decompressZlib(byte[] data) {
    Inflater inflater = new Inflater();   
		inflater.setInput(data);  
		
		ByteArrayOutputStream outputStream = new ByteArrayOutputStream(data.length);  
		byte[] buffer = new byte[1024];
		
		while (!inflater.finished()) {  
			int count = inflater.inflate(buffer);  
			outputStream.write(buffer, 0, count);  
		}  
    
		outputStream.close();  

		return new String(outputStream.toByteArray());
  }
```
