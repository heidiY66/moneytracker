<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>简约记账本</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'PingFang SC', 'Microsoft YaHei', sans-serif;
        }
        
        :root {
            --primary: #4361ee;
            --income: #06d6a0;
            --expense: #ef476f;
            --light: #f8f9fa;
            --dark: #212529;
            --gray: #6c757d;
            --border: #e9ecef;
        }
        
        body {
            background: linear-gradient(135deg, #f5f7fa 0%, #e4edf5 100%);
            color: var(--dark);
            line-height: 1.6;
            padding: 20px 15px 80px;
            min-height: 100vh;
            max-width: 500px;
            margin: 0 auto;
        }
        
        .header {
            text-align: center;
            margin-bottom: 25px;
            padding: 20px 0;
            position: relative;
        }
        
        .header h1 {
            font-size: 28px;
            font-weight: 700;
            color: var(--primary);
            letter-spacing: 1px;
            margin-bottom: 5px;
        }
        
        .header p {
            color: var(--gray);
            font-size: 15px;
        }
        
        .balance-container {
            background: white;
            border-radius: 18px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.05);
            padding: 25px;
            margin-bottom: 25px;
            text-align: center;
        }
        
        .balance-title {
            font-size: 16px;
            color: var(--gray);
            margin-bottom: 8px;
        }
        
        .balance-amount {
            font-size: 40px;
            font-weight: 700;
            letter-spacing: 1px;
            margin: 5px 0;
        }
        
        .summary {
            display: flex;
            justify-content: space-around;
            margin-top: 20px;
            padding-top: 20px;
            border-top: 1px solid var(--border);
        }
        
        .income-box, .expense-box {
            text-align: center;
            flex: 1;
        }
        
        .income-title, .expense-title {
            font-size: 14px;
            margin-bottom: 5px;
        }
        
        .income-amount {
            color: var(--income);
            font-weight: 600;
            font-size: 22px;
        }
        
        .expense-amount {
            color: var(--expense);
            font-weight: 600;
            font-size: 22px;
        }
        
        .transaction-form {
            background: white;
            border-radius: 18px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.05);
            padding: 25px;
            margin-bottom: 25px;
        }
        
        .form-title {
            font-size: 20px;
            font-weight: 600;
            margin-bottom: 20px;
            color: var(--dark);
            text-align: center;
        }
        
        .form-group {
            margin-bottom: 18px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: var(--dark);
        }
        
        .form-control {
            width: 100%;
            padding: 14px 15px;
            border: 2px solid var(--border);
            border-radius: 12px;
            font-size: 16px;
            transition: border-color 0.3s;
        }
        
        .form-control:focus {
            outline: none;
            border-color: var(--primary);
        }
        
        .type-toggle {
            display: flex;
            margin: 15px 0 20px;
        }
        
        .type-btn {
            flex: 1;
            padding: 14px;
            text-align: center;
            background: #f1f3f9;
            border: none;
            border-radius: 12px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .type-btn:first-child {
            margin-right: 10px;
        }
        
        .type-btn.active {
            background: var(--primary);
            color: white;
            box-shadow: 0 4px 12px rgba(67, 97, 238, 0.3);
        }
        
        .btn-submit {
            width: 100%;
            padding: 16px;
            background: var(--primary);
            color: white;
            border: none;
            border-radius: 12px;
            font-size: 18px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 4px 15px rgba(67, 97, 238, 0.4);
        }
        
        .btn-submit:hover {
            background: #3251d4;
            transform: translateY(-2px);
        }
        
        .history {
            background: white;
            border-radius: 18px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.05);
            padding: 25px;
        }
        
        .history-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .history-title {
            font-size: 20px;
            font-weight: 600;
            color: var(--dark);
        }
        
        .clear-btn {
            background: none;
            border: none;
            color: var(--gray);
            font-size: 14px;
            cursor: pointer;
            padding: 5px;
        }
        
        .transaction-list {
            list-style: none;
            max-height: 300px;
            overflow-y: auto;
        }
        
        .transaction-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 16px 15px;
            border-bottom: 1px solid var(--border);
            transition: all 0.3s;
        }
        
        .transaction-item:last-child {
            border-bottom: none;
        }
        
        .transaction-item:hover {
            background: #f9fafb;
        }
        
        .transaction-info {
            flex: 1;
        }
        
        .transaction-name {
            font-weight: 500;
            margin-bottom: 4px;
        }
        
        .transaction-date {
            font-size: 13px;
            color: var(--gray);
        }
        
        .transaction-amount {
            font-weight: 600;
            font-size: 18px;
        }
        
        .income .transaction-amount {
            color: var(--income);
        }
        
        .expense .transaction-amount {
            color: var(--expense);
        }
        
        .delete-btn {
            background: #f8f9fa;
            border: none;
            color: var(--gray);
            width: 36px;
            height: 36px;
            border-radius: 50%;
            margin-left: 15px;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .delete-btn:hover {
            background: #ff6b6b;
            color: white;
        }
        
        .no-transactions {
            text-align: center;
            padding: 30px 0;
            color: var(--gray);
        }
        
        .no-transactions i {
            font-size: 40px;
            margin-bottom: 15px;
            opacity: 0.3;
        }
        
        @media (max-width: 400px) {
            .balance-amount {
                font-size: 32px;
            }
            
            .income-amount, .expense-amount {
                font-size: 18px;
            }
        }
    </style>
</head>
<body>
    <!-- 头部 -->
    <div class="header">
        <h1><i class="fas fa-wallet"></i> 简约记账本</h1>
        <p>记录每一笔收支，掌握财务状况</p>
    </div>
    
    <!-- 余额概览 -->
    <div class="balance-container">
        <div class="balance-title">当前余额</div>
        <div class="balance-amount">¥ 8,450.00</div>
        
        <div class="summary">
            <div class="income-box">
                <div class="income-title">总收入</div>
                <div class="income-amount">¥ 12,560.00</div>
            </div>
            <div class="expense-box">
                <div class="expense-title">总支出</div>
                <div class="expense-amount">¥ 4,110.00</div>
            </div>
        </div>
    </div>
    
    <!-- 记账表单 -->
    <div class="transaction-form">
        <div class="form-title">添加新记录</div>
        
        <div class="form-group">
            <label for="description">收支说明</label>
            <input type="text" id="description" class="form-control" placeholder="例如：工资、餐饮、购物...">
        </div>
        
        <div class="form-group">
            <label for="amount">金额 (¥)</label>
            <input type="number" id="amount" class="form-control" placeholder="输入金额">
        </div>
        
        <div class="type-toggle">
            <button type="button" class="type-btn active" data-type="income">收入</button>
            <button type="button" class="type-btn" data-type="expense">支出</button>
        </div>
        
        <div class="form-group">
            <label for="category">分类</label>
            <select id="category" class="form-control">
                <option value="salary">工资薪水</option>
                <option value="investment">投资理财</option>
                <option value="food">餐饮美食</option>
                <option value="shopping">购物消费</option>
                <option value="transport">交通出行</option>
                <option value="entertainment">休闲娱乐</option>
                <option value="other">其他</option>
            </select>
        </div>
        
        <button class="btn-submit">添加记录</button>
    </div>
    
    <!-- 历史记录 -->
    <div class="history">
        <div class="history-header">
            <div class="history-title">收支记录</div>
            <button class="clear-btn">清空记录</button>
        </div>
        
        <ul class="transaction-list">
            <li class="transaction-item income">
                <div class="transaction-info">
                    <div class="transaction-name">工资收入</div>
                    <div class="transaction-date">2023-06-05 | 工资薪水</div>
                </div>
                <div class="transaction-amount">+ ¥8,500.00</div>
                <button class="delete-btn"><i class="fas fa-times"></i></button>
            </li>
            
            <li class="transaction-item expense">
                <div class="transaction-info">
                    <div class="transaction-name">超市购物</div>
                    <div class="transaction-date">2023-06-10 | 购物消费</div>
                </div>
                <div class="transaction-amount">- ¥256.80</div>
                <button class="delete-btn"><i class="fas fa-times"></i></button>
            </li>
            
            <li class="transaction-item expense">
                <div class="transaction-info">
                    <div class="transaction-name">朋友聚餐</div>
                    <div class="transaction-date">2023-06-12 | 餐饮美食</div>
                </div>
                <div class="transaction-amount">- ¥198.00</div>
                <button class="delete-btn"><i class="fas fa-times"></i></button>
            </li>
            
            <li class="transaction-item income">
                <div class="transaction-info">
                    <div class="transaction-name">理财收益</div>
                    <div class="transaction-date">2023-06-15 | 投资理财</div>
                </div>
                <div class="transaction-amount">+ ¥1,200.00</div>
                <button class="delete-btn"><i class="fas fa-times"></i></button>
            </li>
            
            <li class="transaction-item expense">
                <div class="transaction-info">
                    <div class="transaction-name">加油费</div>
                    <div class="transaction-date">2023-06-18 | 交通出行</div>
                </div>
                <div class="transaction-amount">- ¥350.00</div>
                <button class="delete-btn"><i class="fas fa-times"></i></button>
            </li>
        </ul>
    </div>

    <script>
        // 切换收入/支出类型
        const typeButtons = document.querySelectorAll('.type-btn');
        typeButtons.forEach(button => {
            button.addEventListener('click', () => {
                typeButtons.forEach(btn => btn.classList.remove('active'));
                button.classList.add('active');
            });
        });
        
        // 添加新记录
        const submitButton = document.querySelector('.btn-submit');
        submitButton.addEventListener('click', function() {
            const description = document.getElementById('description').value;
            const amount = document.getElementById('amount').value;
            const category = document.getElementById('category').value;
            const type = document.querySelector('.type-btn.active').dataset.type;
            
            if (!description || !amount) {
                alert('请填写完整信息');
                return;
            }
            
            alert(`记录添加成功！\n类型: ${type === 'income' ? '收入' : '支出'}\n说明: ${description}\n金额: ¥${amount}\n分类: ${document.querySelector(`#category option[value="${category}"]`).textContent}`);
            
            // 实际应用中这里会将记录添加到列表并更新余额
            document.getElementById('description').value = '';
            document.getElementById('amount').value = '';
        });
        
        // 删除记录
        const deleteButtons = document.querySelectorAll('.delete-btn');
        deleteButtons.forEach(button => {
            button.addEventListener('click', function() {
                const item = this.closest('.transaction-item');
                if (confirm('确定要删除这条记录吗？')) {
                    item.style.opacity = '0';
                    setTimeout(() => {
                        item.remove();
                    }, 300);
                }
            });
        });
        
        // 清空记录
        const clearButton = document.querySelector('.clear-btn');
        clearButton.addEventListener('click', function() {
            if (confirm('确定要清空所有记录吗？此操作不可恢复。')) {
                const list = document.querySelector('.transaction-list');
                list.innerHTML = '<div class="no-transactions"><i class="fas fa-receipt"></i><p>暂无收支记录</p></div>';
            }
        });
    </script>
</body>
</html>
