
棋盘从右向左是 1-9

棋子表示：
红方前缀：r （红）
置文前缀：b （黑）

帅-将（K） king
仕-士（A） advisor
相-象（B/E） bishop/elephant
马-马（N/H） knight/horse
车-车（R）   root
炮-炮（C）   cannon
兵-卒（P）   pawn


试验阶段，棋盘和棋子数据使用 Squares[256], Pieces[48];

即1位表示红子(16)，1位表示黑子(32)。因此0到16没有作用，16到31代表红方棋子(16代表帅，17和18代表仕，依此类推，直到27到31代表兵)，32到47代表黑方棋子(在红方基础上加16)。这样，棋盘数组Squares[256]中的每个元素的意义就明确了，0代表没有棋子，16到31代表红方棋子，32到47代表黑方棋子。这样表示的好处就是：它可以快速判断棋子的颜色，(Piece & 16)可以判断是否为红方棋子，(Piece & 32)可以判断是否为黑方棋子。
　　“屏蔽位”的设计不仅仅限制在判断红方棋子还是黑方棋子，如果在棋子数组上再多加7个屏蔽位，就可以对每个兵种作快速判断，例如判断是否是红兵，不需要用(Piece >= 27 && Piece <= 31)，而只要简单的(Piece & WhitePawnBitMask)即可。这样的话，棋子数组的大小就增加到2^12=4096个了，其中9个屏蔽位，还有3位表示同兵种棋子的编号(注意兵有5个，所以必须占据3位)。事实上，确实有象棋程序是使用Pieces[4096]的。


棋盘大小为521x577,每个棋子为57x57, 每个棋子的位置是 5+57*0 ..., 5+57*9,这是
横向.

被选中后的棋子只需要再画一个oos.png选中图片即可。吃子后再重画界面。选中取消
则将选中的棋子重画。
