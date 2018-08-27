# Problem

Given a file path containing "./" and "../", convert the path to a unix standard file path that does not contain "./" and "../".
```
"./"과 "../" 이 포함된 파일 경로를 "./"과 "../"이 없는 유닉스 파일 경로로 바꾸시오.
"./"는 현재의 위치를 뜻하고, "../"는 상위 디렉토리를 뜻합니다.

input: "/usr/bin/../"
output: "/usr/"

input: "/usr/./bin/./test/../"
output: "/usr/bin/"
```

# Solution
1. `"/"`로 split해서 보면 `["", "usr", "bin", ".", "test", ".."]` 와 같은 배열로 만들 수 있다.(ex, input: "/usr/bin/./test/../")
2. stack 자료구조를 이용하여, 유효한 file paths만 stack에 남게 한다.<br/>
  2.1. `""`, `"."`인 경우는 건너뛴다.<br/>
  2.2. `".."`인 경우는 stack에서 pop.<br/>
  2.3. 나머지 다른 경우는 stack에 push.<br/>
3. stack에 남은 file paths를 다시 조합한다.

```java
String convertToUnixPath(String filePath) {
    Stack<String> dirs = new Stack<String>();
    String[] oldDirs = filePath.split("/");
    for(String dir : oldDirs) {
      if("..".equals(dir)) {
        dirs.pop();
      } else if (!(".".equals(dir) || "".equals(dir))) {
        dirs.push(dir);
      }
    }

    final int SIZE = dirs.size();
    String newPath = "";
    for(int i = 0; i < SIZE; ++i) {
      newPath = dirs.pop() + "/" + newPath;
    }
    return "/" + newPath;
```

Time complexity: O(N)

Space complexity: O(N)
