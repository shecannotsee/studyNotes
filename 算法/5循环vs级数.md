1.��һ��
    for ( int i = 0 ; i < n ; i++ )
    for ( int j = 0 ; j < n ; j++ )
        Opeartion ( i,j) ;

    ����������n+n+...+n = n*n = O(n^2)

2.�ڶ���

    for ( int i = 0 ; i < n ; i++ )
    for ( int j = 0 ; j < i ; j++ )
        Opeartion ( i,j) ;

    ����������0+1+...+(n-1) = n(n-1)/2 =O(n^2)

3.������

    for ( int i = 0 ; i < n ; i++ )
    for ( int j = 0 ; j < i ; j += 2020 )
        Opeartion ( i,j) ;

    ����������... =O(n^2)

4.������

    for ( int i = 0 ; i < n ; i <<= 1 )
    for ( int j = 0 ; j < i ; j++ )
        Opeartion ( i,j) ;

    ���μ�����1+2+4+...+ 2^( ȡ������log��Ϊ2����Ϊ(n-1) ) = 2^(ȡ������log��2Ϊ��nΪ����) -1 = O(n)

