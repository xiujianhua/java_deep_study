


课程内容
1. mybatis 知识图谱介绍
    - mybatis 知识
        * 如何写dao代码
            * 原始dao开发
                * dao接口和实现类
            * mapper代理开发方式
                * mapper接口
        * 如何配置
            * 全局配置（一次性配置）
                * 数据源
            * 映射配置
                * 输入映射&输出映射
                * 动态sql标签
                * 二级缓存配置
                * 关联映射配置
                * 延迟加载配置
    - mybatis generator(逆向工程)
    - mybatis plus(mp)
    - tk.mybatis(通用mapper)
    - PageHelper
2. mybatis架构原理
3. mybatis手写框架分析
    - 解析流程
        - 全局配置文件mybatis-config.xml
            - 数据源
            - 关联配置映射文件
        - 映射文件UserMapper.xml---封装多个MapperStatement对象（一个select标签对应一个MapperStatement对象，这些MappedStatement对象都需要封装到Configuration对象中）
            - SQL语句（不是一个JDBC拿来即用的SQL语句，他【需要特殊处理】）
            - 输入参数java类型
            - 输出结果java类型、
            - statementType: 不配置的话，默认就是PrepareStatement
    - 执行流程
        - 获取Connection连接（找Configuraton对象要数据源信息  ，然后通过数据源对象获取连接）
        - 获取sql语句（通过Configuration找MappedStatement对象，通多MappedStatement对象，获取SQL语句【需要特殊处理】）
        - 创建 statement(根据MappedStatement中的Statement需求去创建PreparedStatement,CallableStatement,Statement)
        - 设置参数(需要从MappedStatement对象中获取入参类型，方便知道如何从入参对象中去获取参数)
            - 比如 入参类型是String 直接把值设置到？
            - 比如 入参类型是map 需要更加参数名称获取Map中指定的key的值
        - 向数据库发出sql执行查询，查询出结果集
        - 遍历查询结果集
        - 释放资源