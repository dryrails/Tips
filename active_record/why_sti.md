
### Rails 里面的 STI

```ruby
class Order < ApplicationRecord
  # attr :number 订单都有一个订单编号
  
  before_create do 
    self.number = init_number
  end
  
  protected
  def build_number_suffix
  end
end

class SalesOrder < Order

  belongs_to :saler, foreign_key: 'user_id', class_name: 'Saler'
  
  after_create_commit do 
    increase_property
   
  end

  protected
  
  def increase_property      # 增加公司财产
  end
  
  def notice_sales_warehouse # 通知销售仓库发货
  end
  
  def init_number
    'SO' << build_number_suffix
  end
end

class PurchaseOrder < Order

  belongs_to :purchaser, foreign_key: 'user_id', class_name: 'Purchaser'
 
  protected
  
  def decrease_property 	 # 减少公司账面财产
  end
  
  def notice_purchase_warehouse # 通知采购仓库跟踪货物物流
  end
  
  def init_number
    'PO' << build_number_suffix
  end
end
``` 
