from decimal import Decimal, getcontext
import math

# 设置高精度上下文，因为连分数对精度非常敏感
# 如果你计算 PI 的前 100 项连分数，普通的 float 会迅速失效
getcontext().prec = 100

def gen_continued_fraction(num_input, max_terms=20, tolerance=1e-20):
    """
    一个 Python 生成器 (Generator)，逐个产出连分数的系数 a_n。
    
    Args:
        num_input (str/float/Decimal): 输入的数字。
        max_terms (int): 最大迭代次数，防止无理数无限循环。
        tolerance (float): 容差，当小数部分极小时停止。
        
    Yields:
        int: 下一个连分数系数 a_n
    """
    
    # 转换为 Decimal 以保证精度
    if isinstance(num_input, (int, float)):
        x = Decimal(str(num_input))
    else:
        x = Decimal(num_input)
        
    for _ in range(max_terms):
        # 1. 取整数部分 a_n
        a_n = int(x)
        yield a_n
        
        # 2. 取小数部分
        fractional_part = x - a_n
        
        # 3. 检查是否结束（小数部分接近0）
        if fractional_part < tolerance:
            break
            
        # 4. 连分数核心迭代: x_new = 1 / fractional_part
        x = Decimal(1) / fractional_part

def get_convergent(coeffs):
    """
    根据给定的系数列表，计算当前的渐进分数 p/q。
    输入 [a0, a1, a2] -> 计算 a0 + 1/(a1 + 1/a2)
    """
    if not coeffs:
        return 0, 1
        
    # 从列表末尾倒推计算
    # 初始值设为最后一项: h/k = a_n / 1
    h = coeffs[-1]
    k = 1
    
    # 从倒数第二项向前遍历
    for a in reversed(coeffs[:-1]):
        # h_new = a * h + k
        # k_new = h
        h, k = a * h + k, h
        
    return h, k

# --- 使用示例 ---

def analyze_number(target_str, max_terms=10):
    print(f"\n正在分析数字: {target_str}")
    print(f"目标精度: {getcontext().prec} 位")
    print("-" * 60)
    print(f"{'项数 (n)':<5} | {'系数 (a_n)':<10} | {'当前渐进分数':<20} | {'误差'}")
    print("-" * 60)
    
    coeffs = []
    target_val = Decimal(target_str)
    
    # 实例化生成器
    generator = gen_continued_fraction(target_str, max_terms=max_terms)
    
    for i, a_n in enumerate(generator):
        coeffs.append(a_n)
        
        # 还原分数
        num, den = get_convergent(coeffs)
        current_val = Decimal(num) / Decimal(den)
        error = abs(current_val - target_val)
        
        print(f"{i:<5} | {a_n:<10} | {num}/{den:<20} | {error:.2e}")
        
    print("-" * 60)
    print(f"最终连分数表示: [{coeffs[0]}; {', '.join(map(str, coeffs[1:]))}]")

if __name__ == "__main__":
    # 示例 1: 你之前提到的 6.901
    analyze_number("6.901", max_terms=8)
    
    # 示例 2: 著名的 PI (3.14159...)
    # 注意：这里用字符串传入高精度 PI，如果用 math.pi 会在第 15 位后丢失精度
    pi_str = "3.1415926535897932384626433832795028841971"
    analyze_number(pi_str, max_terms=8)
    
    # 示例 3: 黄金分割率 (1.618...) -> 最优美的连分数 [1; 1, 1, 1...]
    phi_str = "1.61803398874989484820458683436563811772" 
    analyze_number(phi_str, max_terms=8)
