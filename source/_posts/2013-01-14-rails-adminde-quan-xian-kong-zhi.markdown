---
layout: post
title: "rails_admin的权限控制"
date: 2013-01-14 14:32
comments: true
categories: ruby rails_admin cancan
---

rails_admin的权限控制中心

先在rails_admin的配置文件写入

```ruby
RailsAdmin.config do |config|
  config.authorize_with :cancan
end
```

之后使用rails 生成器生成cancan的控制文件,编辑文件
```ruby
class Ability
  include CanCan::Ability

  def initialize(user)
    user ||= User.new
    if user && user.is_superadmin?
      can :access, :rails_admin   #打开路由
      can :dashboard   #打开统计表
      can :manage, :all #这个角色可以读取所有的表
    elsif user.is_admin?
      can :access, :rails_admin 
      can :dashboard
      can :manage, [Person] # 这个用户只能管理这个模型
    end
  end
end
```

