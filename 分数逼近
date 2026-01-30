
def find_best_2digit_fractions(target_float, top_n=10):
    """
    遍历所有两个两位数（10-99）的比值，找出最接近目标小数的分数。
    
    Args:
        target_float (float): 用户输入的目标小数
        top_n (int): 显示前几名最接近的结果
    """
    
    # 两位数的范围是 10 到 99
    min_val = 10
    max_val = 99
    
    results = []

    # 1. 暴力遍历所有可能的组合
    # 分子 (numerator) 从 10 到 99
    for numerator in range(min_val, max_val + 1):
        # 分母 (denominator) 从 10 到 99
        for denominator in range(min_val, max_val + 1):
            
            value = numerator / denominator
            
            # 计算误差（绝对值）
            diff = abs(value - target_float)
            
            # 存储结果：(误差, 分子, 分母, 实际值)
            results.append((diff, numerator, denominator, value))

    # 2. 排序：按误差从小到大排序
    results.sort(key=lambda x: x[0])

    # 3. 输出结果
    print(f"\n目标小数: {target_float}")
    print(f"搜索范围: 分子分母均为 {min_val}-{max_val}")
    print("-" * 65)
    print(f"{'排名':<5} | {'分数':<10} | {'实际值':<15} | {'误差':<15}")
    print("-" * 65)

    # 为了避免输出重复的值（例如 20/20 和 10/10 是一样的），我们去重
    seen_values = set()
    count = 0
    
    for diff, num, den, val in results:
        if val in seen_values:
            continue
            
        seen_values.add(val)
        count += 1
        
        # 格式化输出
        print(f"{count:<5} | {num}/{den:<7} | {val:<15.6f} | {diff:.8f}")
        
        if count >= top_n:
            break

if __name__ == "__main__":
    try:
        user_input = input("请输入一个小数 (例如 6.901): ")
        target = float(user_input)
        
        # 简单的范围检查提示
        if target > 9.9 or target < 0.101:
            print("\n⚠️ 提示: 两位数相除的最大值是 99/10=9.9，最小值约 0.1。")
            print("您的输入可能超出了两位数分数的表达范围，结果可能偏差较大。\n")
            
        find_best_2digit_fractions(target)
        
    except ValueError:
        print("输入错误，请输入一个有效的数字。")
