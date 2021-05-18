1.第一种
    for ( int i = 0 ; i < n ; i++ )
    for ( int j = 0 ; j < n ; j++ )
        Opeartion ( i,j) ;

    算术级数：n+n+...+n = n*n = O(n^2)

2.第二种

    for ( int i = 0 ; i < n ; i++ )
    for ( int j = 0 ; j < i ; j++ )
        Opeartion ( i,j) ;

    算术级数：0+1+...+(n-1) = n(n-1)/2 =O(n^2)

3.第三种

    for ( int i = 0 ; i < n ; i++ )
    for ( int j = 0 ; j < i ; j += 2020 )
        Opeartion ( i,j) ;

    算术级数：... =O(n^2)

4.第四种

    for ( int i = 0 ; i < n ; i <<= 1 )
    for ( int j = 0 ; j < i ; j++ )
        Opeartion ( i,j) ;

    几何级数：1+2+4+...+ 2^( 取下整数log底为2对数为(n-1) ) = 2^(取上整数log以2为底n为对数) -1 = O(n)

