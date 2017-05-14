package web;

import java.awt.Color;
import java.awt.Cursor;
import java.awt.Font;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;

import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JLabel;
import javax.swing.JPanel;

@SuppressWarnings("serial")
public class analizePanel extends JPanel {
	private JLabel title,num,logn,logt,logs,isA,sel;
	private JButton out;
	private ImageIcon NotS = new ImageIcon("NotS.png"); 
	private ImageIcon GetS = new ImageIcon("GetS.png");
	private ImageIcon lastPage = new ImageIcon("lastPage.png");
	private ImageIcon nextPage = new ImageIcon("nextPage.png");
	getInfo getinfo = new getInfo();
	String formerlog = getinfo.getinfo();
	private String[] s = formerlog.split(" ");
	private int row = 0,Labelnum = s.length/5*6,flag=0,start = 0, end = 59,currentPage = 1;
	private int page = Labelnum/60+1;
	JLabel[] label = new JLabel[Labelnum];
	JLabel[] pages = new JLabel[page+2];
	Font font = new Font("微软雅黑", Font.PLAIN, 14);
	Color color1 = new Color(70, 131, 253);
	Color color2 = new Color(222, 232, 250);
	public analizePanel() {
		setSize(800, 430);
		setLayout(null);
		setBackground(Color.white);
		title = new JLabel("共            " + Labelnum/6 + "         条记录");
		title.setFont(font);
		title.setBounds(80, 25, 200, 20);
		num = new JLabel("编号", JLabel.CENTER);
		num.setFont(font);
		num.setBounds(80, 50, 70, 20);
		num.setOpaque(true);
		num.setBackground(color1);
		num.setForeground(Color.white);
		
		logn = new JLabel("文件名", JLabel.CENTER);
		logn.setFont(font);
		logn.setBounds(150, 50, 150, 20);
		logn.setOpaque(true);
		logn.setBackground(color1);
		logn.setForeground(Color.white);
		
		logt = new JLabel("分析时间", JLabel.CENTER);
		logt.setFont(font);
		logt.setBounds(300, 50, 150, 20);
		logt.setOpaque(true);
		logt.setBackground(color1);
		logt.setForeground(Color.white);
		
		logs = new JLabel("文件大小(KB)", JLabel.CENTER);
		logs.setFont(font);
		logs.setBounds(450, 50, 130, 20);
		logs.setOpaque(true);
		logs.setBackground(color1);
		logs.setForeground(Color.white);
		
		isA = new JLabel("存在攻击", JLabel.CENTER);
		isA.setFont(font);
		isA.setBounds(580, 50, 80, 20);
		isA.setOpaque(true);
		isA.setBackground(color1);
		isA.setForeground(Color.white);
		
		sel = new JLabel("选择", JLabel.CENTER);
		sel.setFont(font);
		sel.setBounds(660, 50, 80, 20);
		sel.setOpaque(true);
		sel.setBackground(color1);
		sel.setForeground(Color.white);
		//左箭头和右箭头
		pages[0] = new JLabel(lastPage);
		pages[0].setBounds(610,25,20,20);
		add(pages[0]);
		pages[page+1] = new JLabel(nextPage);
		pages[page+1].setBounds(710,25,20,20);
		add(pages[page+1]);
		if(page > 1){
			pages[0].addMouseListener(new leftPage());
			pages[0].setCursor(new Cursor(Cursor.HAND_CURSOR));
			pages[page+1].addMouseListener(new rightPage());
			pages[page+1].setCursor(new Cursor(Cursor.HAND_CURSOR));
		}
		if (page == 1) {
			pages[1] = new JLabel("1");
			pages[1].setBounds(665, 20, 30, 30);
			add(pages[1]);
		}
		if (page == 2) {
			pages[1] = new JLabel("1");
			pages[1].setBounds(650, 20, 30, 30);
			pages[1].addMouseListener(new Click());
			pages[1].setCursor(new Cursor(Cursor.HAND_CURSOR));
			add(pages[1]);
			pages[2] = new JLabel("2");
			pages[2].setBounds(680, 20, 30, 30);
			pages[2].addMouseListener(new Click());
			pages[2].setCursor(new Cursor(Cursor.HAND_CURSOR));
			add(pages[2]);
		}
		if (page == 3){
			pages[1] = new JLabel("1");
			pages[1].setBounds(635, 20, 30, 30);
			add(pages[1]);
			pages[2] = new JLabel("2");
			pages[2].setBounds(665, 20, 30, 30);
			add(pages[2]);
			pages[3] = new JLabel("3");
			pages[3].setBounds(695, 20, 30, 30);
			add(pages[3]);
		}
		if(page > 3){
			
		}
		if(Labelnum <= 60){
			drawTable(0, Labelnum);
		}else{
			drawTable(0, 59);
		}
		out = new JButton("导出");
		out.setFont(font);
		out.setBackground(new Color(250, 250, 250));
		out.setBounds(635, 330, 85, 30);
		out.setForeground(new Color(153, 153, 153));
		out.addActionListener(new out());
		add(num);
		add(logn);
		add(logt);
		add(logs);
		add(isA);
		add(sel);
		add(title);
		add(out);
	}
	
	public class LabelClick extends MouseAdapter {
		@Override
		public void mouseClicked(MouseEvent e) {
			if (e.getSource() == label[5]&&flag == 0){
				flag = 1;
				 //the label clicked is set to red, other labels are black
//				firstLabel.setForeground(Color.red);
//				secondLabel.setForeground(Color.black);
				// show the first panel
				// 把要显示的面板放入指定区域
//				if (!firstPanel.isVisible()) {
//					MainSurface.this.add(firstPanel, BorderLayout.CENTER);
//					firstPanel.setVisible(true);
//				}
				//System.out.println(1);
				label[5].setIcon(GetS);
				 //原先显示的面板设置为不可见
				//secondPanel.setVisible(false);
			} else if (e.getSource() == label[5]&&flag == 1) {
				flag = 0;
				 //the label clicked is set to red, other labels are black
//				secondLabel.setForeground(Color.red);
//				firstLabel.setForeground(Color.black);
//				// show the second panel
//				if (!secondPanel.isVisible()) {
//					MainSurface.this.add(secondPanel, BorderLayout.CENTER);
//					secondPanel.setVisible(true);
//				}
				label[5].setIcon(NotS);
//				firstPanel.setVisible(false);
			}
		}
	}
	
	private class out implements ActionListener{
		@Override
		public void actionPerformed(ActionEvent e) {
			// TODO Auto-generated method stub
			out.setBackground(new Color(70, 131, 253));
			out.setForeground(new Color(250, 250, 250));
		}
	}
	
	public class Click extends MouseAdapter{
		@Override
		public void mouseClicked(MouseEvent e){
			if(e.getSource() == pages[1]){
				clear(Labelnum);
				drawTable(0, 59);
			}
			
			if(e.getSource() == pages[2]){
				clear(60);
				drawTable(60, Labelnum);
			}
		}
	}
	public void clear(int lastPosition){
		for(int i = 0; i<lastPosition; ++i){
			if((i+1)%6 != 0){
			label[i].setText("");
			label[i].setBackground(Color.white);
			}
			if((i+1)%6 == 0){
				label[i].setIcon(null);
			}
		}
	}
	public void drawTable(int start, int Labelnum){
	row = 0;
	for(int i=start, j=(start/6*5); i<=Labelnum; i+=6,j+=5){
		label[i] = new JLabel(""+(i/6+1), JLabel.CENTER);
		label[i].setFont(font);
		label[i].setBounds(80,70+row*25,70,25);
		if(row%2 == 1){
			label[i].setOpaque(true);
			label[i].setBackground(color2);}
		add(label[i]);
		
		label[i+1] = new JLabel(s[j], JLabel.CENTER);
		label[i+1].setFont(font);
		label[i+1].setBounds(150,70+row*25,150,25);
		if(row%2 == 1){
			label[i+1].setOpaque(true);
			label[i+1].setBackground(color2);}
		add(label[i+1]);
		
		label[i+2] = new JLabel(s[j+1]+"  "+s[j+2], JLabel.CENTER);
		label[i+2].setFont(font);
		label[i+2].setBounds(300,70+row*25,150,25);
		if(row%2 == 1){
			label[i+2].setOpaque(true);
			label[i+2].setBackground(color2);}
		add(label[i+2]);
		
		label[i+3] = new JLabel(s[j+3], JLabel.CENTER);
		label[i+3].setFont(font);
		label[i+3].setBounds(450,70+row*25,130,25);
		if(row%2 == 1){
			label[i+3].setOpaque(true);
			label[i+3].setBackground(color2);}
		add(label[i+3]);
		
		label[i+4] = new JLabel(s[j+4], JLabel.CENTER);
		label[i+4].setFont(font);
		label[i+4].setBounds(580,70+row*25,80,25);
		if(row%2 == 1){
			label[i+4].setOpaque(true);
			label[i+4].setBackground(color2);}
		add(label[i+4]);
		
		label[i+5] = new JLabel(NotS);
		label[i+5].setBounds(685, 70+row*25, 30,25);
		label[i+5].setCursor(new Cursor(Cursor.HAND_CURSOR)); // 当鼠标移到标签上时显示手型图标
		label[i+5].addMouseListener(new LabelClick());
		add(label[i+5]);
		row++;
	}
	}
	
	private class leftPage extends MouseAdapter{

	}
	
	private class rightPage extends MouseAdapter{

	}
}

/*
int column = s.length / 5 + 1;
table = new JTable(column, 5);

// 设置行高
table.setRowHeight(30);
table.setBorder(BorderFactory.createLineBorder(Color.black));
table.setBounds(80, 50, 600, 30 * column);
table.setBackground(Color.LIGHT_GRAY);
// 设置单元格文字居中
DefaultTableCellRenderer r = new DefaultTableCellRenderer();
r.setHorizontalAlignment(JLabel.CENTER);
table.setDefaultRenderer(Object.class, r);
TableModel m = table.getModel();
m.setValueAt("文件名", 0, 1);
m.setValueAt("时间", 0, 2);
m.setValueAt("文件大小（KB）", 0, 3);
m.setValueAt("是否存在攻击", 0, 4);
m.setValueAt("编号", 0, 0);
m.setValueAt("分析日期", 0, 1);
m.setValueAt("文件大小（KB）", 0, 2);
m.setValueAt("存在攻击", 0, 3);
m.setValueAt("选择", 0, 4);
for (int i = 0, j = 1; i < s.length && j <= s.length / 5; i += 5, ++j) {
	m.setValueAt(j, j, 0);
	//m.setValueAt(s[i], j, i % 5 + 1);
	m.setValueAt(s[i + 1]+ " " + s[i + 2], j, i % 5 + 1);
	m.setValueAt(s[i + 1] + " " + s[i + 2], j, i % 5 + 2);
	m.setValueAt(s[i + 3], j, i % 5 + 3);
	m.setValueAt(s[i + 4], j, i % 5 + 4);
	// System.out.println(j);
	// System.out.println(s[i]);
	// System.out.println(s[i+1]);
	// System.out.println(s[i+3]);
	// System.out.println(s[i+4]);
	// }
}
*/
/*
 * // 创建标题面板 titlePanel = new JPanel();
 * 
 * // 设置标题面板的大小 titlePanel.setPreferredSize(new Dimension(600, 140));
 * 
 * // 设置标题面板上下左右的边距
 * titlePanel.setBorder(BorderFactory.createEmptyBorder(40, 0, 0, 0));
 * 
 * // 设置标题的字体及大小 title = new JLabel("Second Panel",
 * SwingConstants.CENTER); title.setFont(new Font("宋体", Font.BOLD, 28));
 * 
 * // 把标题加入标题面板 titlePanel.add(title);
 * 
 * // 把标题面板加入first panel面板 this.add(titlePanel, BorderLayout.NORTH);
 */
