MOD ( t.key , 5) = 4
这个t.key可以是数字number 也可以是字符串varchar
但是如果是字符串 必须保证所有被查到的数据中 只能是纯数字 否则会报错

// mod函数中表字段可以是数字number 也可以是字符串varchar 但是如果是字符串 必须保证所有被查到的数据中 只能是纯数字 否则会报错 ORA-01722 invalid number

1、清空表，相当于null值；这种情况我测试，不会报错；结果也是null值；  
  
2、我找了VARCHAR2类型的字段测试，查询MOD (TO_NUMBER (字段), 5)，也是成功的；  
  
3、我测试MOD (TO_NUMBER (‘空格’), 5)，会报错ORA-01722: invalid number。
