## 统计每日用户注册数、商品发布数、形成订单数

`
	SELECT
	t1.createTime,
	t1.dcount as 每日注册数,
	t2.gcount as 每日发布商品数,
	t3.ocount as 每日形成订单数
FROM
	(
		SELECT
			DATE_FORMAT(createTime, '%Y-%m-%d') AS createTime,
			count(*) AS dcount
		FROM
			t_user
		GROUP BY
			date(createTime) DESC
	) t1,
	(
		SELECT
			DATE_FORMAT(createTime, '%Y-%m-%d') AS createTime,
			count(*) AS gcount
		FROM
			t_goods_auditing
		GROUP BY
			date(createTime) DESC
	) t2,
		(
		SELECT
			DATE_FORMAT(createTime, '%Y-%m-%d') AS createTime,
			count(*) AS ocount
		FROM
			t_orders
		GROUP BY
			date(createTime) DESC
	) t3
WHERE
	t1.createTime = t2.createTime and t1.createTime = t3.createTime
	`
