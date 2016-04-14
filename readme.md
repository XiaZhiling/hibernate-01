1.如何获取Session对象

	a.SessionFactory.openSession();
	b.SessionFactory.getCurrentSession();
	**使用getCurrentSession需要在hibernate.cfg.xml需要配置hibernate.current_session_context_class属性[thread:使用本地事务  、jta:使用全局事务(Jta事务)]
2.openSession() 与 getCurrentSession()的区别

	a.getCurrentSession在事务的提交和回滚之后会自动关闭，而openSession需要手动关闭(多次未关闭会导致连接池溢出)
	b.openSession每次创建新的session对象，而getCurrentSession使用现有的session对象
3.hbm配置文件常用设置

	<hibernate-mapping 
		schema="" 
		catalog="" 
		default-access="property|noop|field"   //设置访问策略
		default-cascade="none"       //级联风格
		default-lazy="true|false"    //加载策略
		auto-import="true|false" 
		package=""
	>
		<class 
			name="" 
			table=""
			batch-size="N"    //抓取策略  一次可以抓取N条记录
			where="condition"   //抓取条件
			entity-name="EntityName"   //同一个实体类映射成多张表
		>
			<id
				name=
				type
				column
				length
				<generator class="">  //主键生成策略   assigned适用于自然主键，程序负责生成
			></id>
			
			<component name="" class="">  //组件属性
				<property name="" column="">
			</component>
4.创建BLOb类型数据 ： 

	Hibernate.getLobCreate(session).createBlob();
5.session CRUD /get与load的区别

	get/load /update /delete 
	a.在不考虑缓存的情况下，get方法会在调用之后立即向数据库发出sql语句，返回持久化对象，对象不存在 返回null
	b.load方法会在调用后返回个代理对象,该代理对象只保存了实体对象的id,直到使用对象的非主键属性时才会发送sql语句,对象不存在抛出异常
	
			