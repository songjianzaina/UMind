# 文件目录说明：

## 图片目录：/images 

包含运行所需要的图片文件

## 源码目录：/src/version1/

### AddFileChooser.java

负责构造文本选择框

实现文本保存和打开的事件监听

本类 在主窗口菜单 创建“文件”菜单项时实例化

变量

 * private JMenuItem openFile 主菜单栏“打开文件”菜单项
 * private JMenuItem saveFile 主菜单栏“保存文件”菜单项
 * private JFileChooser fileChooser java.swing包里提供的文件选择框

方法

 * public static void loadFile(File file)  打开文件
 * void saveFile(File file)  			     保存文件

### ComponentMouseListener.java

监听主题，并作相应动作 

1. 双击新建主题 

2. 单击连接曲线 

3. 拖动主题及连接线、曲线

4. 右键面板菜单 

5. 鼠标进入主题蒙板

变量

int startX,startY:鼠标起始位置 

ThemeLabel Label:监听主题 

JLabel Mask:主题蒙板 

Boolean isClickLeftAndDrag:是否拖拽模式

### ConnectLine.java

1. 连接线类连接主题，每个主题对应唯一入度 

2. 连接线自动探测连接

属性： 

int StartX,startY:起点坐标

int endX,endY 终点坐标 

int width:线宽 

Color colr:颜色

boolean isLive:状态

### Constent.java

定义了程序使用到的所有常量和风格枚举变量

变量

 * paintPanelWidth paintPanelHight 面板的宽高
 * frameHeight frameWidth 窗口的宽高
 * ThemeSizeX ThemeSizeY 主题默认宽高
 * LabelThickness 主题边框厚度
 * themeFont 主题文字字体
 * themeFrameHeight themeFrameWidth 修改主题窗口宽高
 * imagesPath图片路径
 * minDistancex minDistancey 检测连接线范围
 * addRight addLeft 左右翻转
 * Maskbkg Maskbd 选中边框和高亮色
 * LightGreen Pink DarkPurpule Purpule LightRed 风格Dracula主题色
 * Orange Lime LightGery DarkGrey 风格Sublime主题色
 * public enum StyleEnum 风格枚举型变量

方法

 * private StyleEnum(Color bdcolor,Color bkgcolor,Color txtcolor,
       Color linecolor,Color panelcolor,Color curvelcolor,Color btncolor) 风格枚举构造方法
 * 获取颜色变量的方法 public Color get*()

### CurveLine.java

1. 4个点之间有3条贝塞尔曲线，本类负责保存有关贝塞尔曲线属性
2. 通过右键菜单实现手动连接曲线

### MainWindow.java

 用于构造主窗口（界面）的制作，包括主菜单栏及面板，同时是整个程序的main函数所在文件。

变量

 * public static JFrame frame 主窗口，不使用
 * public static Container frameContainer 主窗口容器，不使用
 * public static PaintePanel pan 所有组件均加入此面板容器，使用绝对布局

方法

 * public static void main(String args[]) main函数
 * public MainWindow() 创建窗口、主菜单、放置组件的pan、及右键菜单
 * public void createMenu() 创建菜单并加入到窗口上端

### nodeListener.java

1. 监听曲线上两个节点JLbel node1,node2; 
2. 移动node1或node2拖动曲线；
3. 右键node1或node2删除曲线。

### PaintePanel.java

继承Jpanel，作为绘画面板组件，是主题类的容器

变量

 * public static RightClickMenu rightClickMenu = null; 右键菜单
 * private ThemeLabel rootThemeLabel = null; 根主题
 * private HashMap<ThemeLabel, ConnectLine> ConnectLineList = null; 主题索引的连接线哈希表
 * private Vector<CurveLine>CurveLineList=null; 关系线向量
 * JScrollPane scrollPane = null; 面板滚动条

方法

 * public PaintePanel() 构造方法，被MainWindow在初始化时创建
 * 关系线操作方法

   public Vector<CurveLine> getcurveLineList()

   public void setCurveLineList(Vector<CurveLine> CurveLineList)

   public void addCurveLine(CurveLine curveLine)
 * 根节点操作方法

   public void rootThemeaddChild(ThemeLabel themeLabel)

   public ThemeLabel getrootThemeLabel()
 * 创建面板右键菜单

   public void CreatBox()
 * 操作连接线

   public void addConnectLine(ThemeLabel themeLabel, ConnectLine connectLine)

   public ConnectLine getConnectLine(ThemeLabel themeLabel)

   public void removeConnectLine(ThemeLabel themeLabel)

   public void removeAllConnectLine()

   public HashMap<ThemeLabel, ConnectLine> getallConnectLine()

   public void setallConnectLine(HashMap<ThemeLabel, ConnectLine> ConnectLineList)
 * 重载JPanel的绘画方法，画主题、连接线和关系线

   public void paint(Graphics g)
 * 实现Runnable接口，10ms刷新面板

   public void run()
 * 更改面板主题

   public void changestyle()

### PaintHelper.java

1. 传入画板中的画笔，实现底层绘画功能；

2. 实现绘制连接线和绘制曲线

### PanMouseListener.java

处理面板上的鼠标事件

变量

 * private boolean isClickRightAndDrag = false;	鼠标右键全局拖动状态
 * public PaintePanel pan = null; 指向全局面板
 * int oldX = 0; int oldY = 0; 鼠标旧坐标

方法

 * public PanMouseListener(PaintePanel pan) 构造方法

   重载的鼠标事件服务函数

 * public void mouseClicked(MouseEvent e) 右击或双击

 * public void mousePressed(MouseEvent e) 按下

 * public void mouseReleased(MouseEvent e) 释放

 * public void mouseDragged(MouseEvent e) 拖动

 * public void clearBoxs() 清除右键菜单

### RightClickMenu.java

主题类对象右键菜单的构造及相应监听功能实现

面板对象右键菜单的构造及相应监听功能实现

节点对象右键菜单的构造及相应监听功能实现

变量

* public JPopupMenu rightMenuForPan 面板对象右键菜单
 * public JPopupMenu rightMenuForComponent 主题类对象右键菜单
 * public JPopupMenu rightMenuForNode 节点对象右键菜单
 * public JComboBox fontTypeBox 字体下拉框
 * public JComboBox fontColorBox 文字颜色下拉框
 * public JComboBox fontSizeBox 文字大小下拉框
 * public static MouseEvent componentE = null 保存产生右键菜单的组件位置
 * public static MouseEvent oldcomponentE = null 用于记录前一产生右键菜单的组件位置，便于连接线的两端的确认
 * public static CurveLine curveLine = null 记录要新建的连接类

方法

 * public RightClickMenu() 初始化三个右键菜单并加上监听
 * public void creatIcons(JMenu menuIcon)  制造图标右键菜单栏
 * public void createBoxs() 制造出字体、颜色、大小的下拉框及相应事件响应
 * public Color parseColor(String color) 将选择颜色的汉字与Color一一对应
 * class ThemeStateChange 实现剪切、复制、粘贴的事件监听

### ThemeChooser.java

风格菜单栏监听

修改风格和保存风格

变量

​	三个风格菜单选项

 * private JMenuItem Dracula;

 * private JMenuItem Sublime;

 * private JMenuItem Classic;

   全局风格变量

 * public static StyleEnum LocalStyle = StyleEnum.Classic; 

方法

 * public ThemeChooser (JMenuItem Dracula,JMenuItem Sublime,JMenuItem Classic) 构造函数，加入选项监听
 * public void actionPerformed(ActionEvent e)  判断动作并更改全局风格

序列化的风格保存类

 * class saveStyle implements java.io.Serializable
 * public saveStyle(StyleEnum localStyle)  风格保存函数

### ThemeDetect.java

1. 本类接收外部传入面板，在该面板上进行底层操作； 

2. 双击新建主题，自动生成连接线； 

3. 右键手动建立曲线；

4. 更新主题、连接线、曲线位置；

5. 移动所有主题、连接线、曲线位置； 

6. 删除主题及其相关连接线、曲线；

7. 删除曲线。

### ThemeFrame.java

负责构造主题内容修改窗口

加入相应监听

变量

 * private ThemeLabel owner = null  从属于子主题类对象
 * private JTextField input = null  主题显示内容修改文本框
 * private JTextArea remark = null  主题备注内容修改多行文本框
 * private JTextField link=null     链接显示内容修改文本框
 * private JButton button1 = null   确认按钮
 * private JButton button2 = null   取消按钮

方法

 * public ThemeFrame(ThemeLabel from) 构造主题内容修改窗口
 * class ThemeFrameActionListener implements ActionListener 确认按钮的事件监听

### ThemeLabel.java

主题类，放置于软件面板，实现基本思维导图绘画功能

变量

 * private int iconNum = 0; 图标编号
 * private ThemeLabel father = null;指向父亲主题
 * private Vector<ThemeLabel> child = null;孩子主题向量
 * private Vector<CurveLine>CurveLineList=null;连接线向量
 * private ThemeFrame myThemeFrame = null;主题修改窗口

   主题尺寸
 * private int ThemeSizeX;
 * private int ThemeSizeY;

   端点坐标
 * private int ThemeLeftX, ThemeRightX, ThemeMidY;
 * private String linkURL =null;超链接地址
 * public boolean isLive = true;是否存活

方法

 * public ThemeLabel(int x, int y)构造函数，将默认主题放置于面板指定坐标

   连接线列表操作
 * public boolean isInTree()
 * public boolean isChild(ThemeLabel themeLabel)
 * public void addChild(ThemeLabel child)
 * public void removeChild(ThemeLabel child)
 * public void setFather(ThemeLabel father)
 * public ThemeLabel getFather()
 * public Vector<ThemeLabel> getallChild()
 * public ThemeLabel getChild(int index) {

   关系线列表操作
 * public Vector<CurveLine> getCurveLineList()
 * public void addCurveLine(CurveLine curveLine)
 * public void removeCurveLine(CurveLine curveLine) 

   更新位置大小文字长度
 * public void updateLocation(int x, int y)
 * public void updateSize()
 * public int getNewLength()

   多级主题显示
 * public int getRank()
 * public void setRank(int Rank)

   更新风格
 * public void setStyle() {

   超链接
 * public String getLinkURL()
 * public void setLinkURL(String linkURL)

   修改窗口
 * public ThemeFrame getMyThemeFrame()
 * public void setMyThemeFrame(ThemeFrame myThemeFrame)