b0VIM 8.2[28622DESKTOP-F7HTF14~28622/Desktop/hmsx/README.md
U3210#"! Utpadßÿÿüûq!

海马生鲜电商项目实战

use hmsc_db;

drop table if exists `user`; create table `user` ( `uid` bigint(20) not null auto_increment comment '用户id', `nickname` varchar(100) not null default '' comment '用户昵称', `mobile` varchar(20) not null default '' comment '手机号码', `email` varchar(100) not null default '' comment '用户邮箱', `sex` tinyint(1) not null default '0' comment '1:男 2:女 0:没有填写', `avatar` varchar(64) not null default '' comment '头像', `login_name` varchar(20) not null default '' comment '登录用户名', `login_pwd` varchar(32) not null default '' comment '登录密码', `login_salt` varchar(32) not null default '' comment '登录密码的随机密钥', `status` tinyint(1) not null default '1' comment '1:有效 0:无效', `updated_time` timestamp not null default current_timestamp comment '最后一次更新时间', `created_time` timestamp not null default current_timestamp comment '创建时间', primary key (`uid`), unique key `login_name` (`login_name`) )ENGINE=InnoDB default charset=utf8 comment='用户表（管理员）';

insert into `user` (`uid`,`nickname`,`mobile`,`email`,`sex`,`avatar`,`login_name`,`login_pwd`,`login_salt`,`status`,`updated_time`,`created_time`) values (1,'BruceNick','13933746521','[Bruce@aliyun.com](mailto:Bruce@aliyun.com)',1,'','Bruce','816440c40b7a9d55ff9eb7b20760862c','cF3JfH5FJfQ8B2Ba',1,'2020-04-23 11:30:30','2020-04-23 11:10:30');

会员表
use hmsc_db;

drop table if exists `member`; create table `member` ( `id` int(11) unsigned not null auto_increment, `nickname` varchar(100) not null default '' comment '会员昵称', `mobile` varchar(20) not null default '' comment '会员手机号码', `sex` tinyint(1) not null default '0' comment '1:男 2:女 0:没有填写', `avatar` varchar(200) not null default '' comment '会员头像', `salt` varchar(32) not null default '' comment '登录密码的随机密钥', `reg_ip` varchar(100) not null default '' comment '注册ip', `status` tinyint(1) not null default '1' comment '1:有效 0:无效', `updated_time` timestamp not null default current_timestamp comment '最后一次更新时间', `created_time` timestamp not null default current_timestamp comment '创建时间', primary key (`id`) )ENGINE=InnoDB default charset=utf8 comment='会员表';

flask-sqlacodegen 'mysql://ljw:950920@127.0.0.1/hmsx_db' --tables member --outfile "common/models/member/Member.py" --flask

insert into `member` (`id`,`nickname`,`mobile`,`sex`,`avatar`,`salt`,`reg_ip`,`status`,`updated_time`,`created_time`) values (1,'BruceNick','13933746521',1,'','cF3JfH5FJfQ8B2Ba','20200429',1,'2020-04-29 11:30:30','2020-04-29 11:10:30');

会员评论
use hmsc_db;

drop table if exists `member_comments`;
create table `member_comments`(
	`id` int(11) unsigned not null auto_increment,
	`member_id` int(11) not null default '0' comment '会员id',
	`goods_id` varchar(200) not null default '' comment '商品id',
	`pay_order_id` int(11) not null default '0' comment '订单id',
	`score` tinyint(4) not null default '0' comment '评分',
	`content` varchar(200) not null default '' comment '评论内容',
	`created_time` timestamp not null default current_timestamp on update current_timestamp comment '创建时间',
	primary key (`id`),
	key `idx_member_id` (`member_id`)
)ENGINE=InnoDB default charset=utf8 comment='会员评论表';

生成model
flask-sqlacodegen 'mysql://ljw:950920@127.0.0.1/hmsx_db' --tables member_comments --outfile "common/models/member/MemberComment.py" --flask

insert into `member_comments` (`id`,`member_id`,`goods_id`,`pay_order_id`,`score`,`content`,`created_time`) values (1,'1','1','1','10','好，good','2020-04-29 11:10:30');