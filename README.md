# dsfevimport numpy as np

# 创建一个15x15的棋盘
board = np.zeros((15, 15), dtype=int)

# 定义棋盘状态常量
EMPTY = 0
BLACK = 1
WHITE = 2

# 定义当前下棋方
current_player = BLACK

# 检查是否存在五子连珠的情况
def check_win(row, col, player):
    # 检查水平方向
    count = 1
    left = col - 1
    while left >= 0 and board[row][left] == player:
        count += 1
        left -= 1

    right = col + 1
    while right < 15 and board[row][right] == player:
        count += 1
        right += 1

    if count >= 5:
        return True

    # 检查垂直方向
    count = 1
    top = row - 1
    while top >= 0 and board[top][col] == player:
        count += 1
        top -= 1

    bottom = row + 1
    while bottom < 15 and board[bottom][col] == player:
        count += 1
        bottom += 1

    if count >= 5:
        return True

    # 检查主对角线方向
    count = 1
    i = row - 1
    j = col - 1
    while i >= 0 and j >= 0 and board[i][j] == player:
        count += 1
        i -= 1
        j -= 1

    i = row + 1
    j = col + 1
    while i < 15 and j < 15 and board[i][j] == player:
        count += 1
        i += 1
        j += 1

    if count >= 5:
        return True

    # 检查副对角线方向
    count = 1
    i = row - 1
    j = col + 1
    while i >= 0 and j < 15 and board[i][j] == player:
        count += 1
        i -= 1
        j += 1

    i = row + 1
    j = col - 1
    while i < 15 and j >= 0 and board[i][j] == player:
        count += 1
        i += 1
        j -= 1

    if count >= 5:
        return True

    return False

# 处理玩家下棋的动作
def make_move(row, col):
    global current_player

    if board[row][col] == EMPTY:
        board[row][col] = current_player

        if check_win(row, col, current_player):
            winner = "黑棋" if current_player == BLACK else "白棋"
            print(f"恭喜，{winner}获胜！")
            # 在MicroOffice Teams上发送获胜消息

        current_player = WHITE if current_player == BLACK else BLACK

# 在MicroOffice Teams上获取玩家的输入并进行处理
def process_input(input):
    # 解析输入，获取玩家下棋的位置坐标
    row = int(input["row"])
    col = int(input["col"])

    make_move(row, col)

# 主循环，等待玩家输入
while True:
    # 在MicroOffice Teams上获取玩家输入
    input = get_player_input()
    process_input(input)
