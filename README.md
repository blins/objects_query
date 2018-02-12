**Objects QuerySet**

QuerySet like django's QuerySet but any iter of objects

Example:

    from objects_query import Q, QuerySet

    class F(): pass
    
    to = F()
    to.id = 2
    to.type = 1
    to.s = 'aaa1111'

    to1 = F()
    to1.id = 1
    to1.type = 3
    to1.s = 'aaa1'

    e = Q(Q(Q(id=3) | Q(id=1)) & ~Q(type=2))
    print(e.evaluate(to))

    e = Q(s__regex = '^aaa\d+')
    print(e.evaluate(to))
    
    q = QuerySet([to, to1])
    qq = q.filter(s__regex = '^aaa\d+')
    qqq = qq.filter(Q(Q(id=3) | Q(id=1)) & ~Q(type=2))
    qqqq = q.exclude(id=2)
    for i in q:
        print(i.__dict__)
