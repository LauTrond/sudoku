# sudoku 数独解题

毫秒级的数独解题，还能显示每一步的推断。

试试：

    $ go get github.com/LauTrond/sudoku
    $ echo "
       7
    1
       43 2
            6
       5 9
          418
        81
      2    5
     4    3
    " | go run github.com/LauTrond/sudoku
    
    ====================================
    <0> start
                | 7          |            
     1          |            |            
                | 4   3      | 2          
    ------------------------------------
                |            |         6  
                | 5       9  |            
                |            | 4   1   8  
    ------------------------------------
                |     8   1  |            
             2  |            |     5      
         4      |            | 3          
    ====================================
    <1> 该行唯一可以填入 1 的单元格
                | 7          |            
     1          |            |            
                | 4   3      | 2      [1] 
    ------------------------------------
                |            |         6  
                | 5       9  |            
                |            | 4   1   8  
    ------------------------------------
                |     8   1  |            
             2  |            |     5      
         4      |            | 3          
    ====================================
    <2> 该行唯一可以填入 1 的单元格
                | 7          |            
     1          |            |            
                | 4   3      | 2       1  
    ------------------------------------
                |            |         6  
                | 5       9  |            
                |            | 4   1   8  
    ------------------------------------
                |     8   1  |            
             2  |            |     5      
         4  [1] |            | 3          

    ....
    
    找到了 1 个解
    ====================================
    result 0
     2   6   4  | 7   1   5  | 8   3   9  
     1   3   7  | 8   9   2  | 6   4   5  
     5   9   8  | 4   3   6  | 2   7   1  
    ------------------------------------
     4   2   3  | 1   7   8  | 5   9   6  
     8   1   6  | 5   4   9  | 7   2   3  
     7   5   9  | 6   2   3  | 4   1   8  
    ------------------------------------
     3   7   5  | 2   8   1  | 9   6   4  
     9   8   2  | 3   6   4  | 1   5   7  
     6   4   1  | 9   5   7  | 3   8   2  

谜题写在txt文件中，可以作为参数来运行：

    $ cd $GOPATH/src/github.com/LauTrond/sudoku
    $ go run . puzzles/2.txt

使用 -h 参数命令选项：

    $ cd $GOPATH/src/github.com/LauTrond/sudoku
    $ go run . -h

同时使用 -stop-at-first -result-only 可以显示运算耗时。

puzzles/0.txt 是搜索引擎上找到的号称"最难的数独题"，耗时约3毫秒：

    $ cd $GOPATH/src/github.com/LauTrond/sudoku
    $ cat puzzles/0.txt
    ..53.....
    8......2.
    .7..1.5..
    4....53..
    .1..7...6
    ..32...8.
    .6.5....9
    ..4....3.
    .....97..
    
    $ go run . -stop-at-first -result-only puzzles/0.txt
    
    找到了 1 个解
    ====================================
    result 0
     1   4   5  | 3   2   7  | 6   9   8  
     8   3   9  | 6   5   4  | 1   2   7  
     6   7   2  | 9   1   8  | 5   4   3  
    ------------------------------------
     4   9   6  | 1   8   5  | 3   7   2  
     2   1   8  | 4   7   3  | 9   5   6  
     7   5   3  | 2   9   6  | 4   8   1  
    ------------------------------------
     3   6   7  | 5   4   2  | 8   1   9  
     9   8   4  | 7   6   1  | 2   3   5  
     5   2   1  | 8   3   9  | 7   6   4  
    
    总耗时：2.922656ms
