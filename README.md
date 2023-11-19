# 1st-try
Line[] lines;  // 直线数组
int numLines;  // 直线数量

void setup() {
  size(800, 600);
  background(0);
  

  // 根据画布尺寸计算直线数量
  numLines = 50;
  
  // 初始化直线数组
  lines = new Line[numLines];
  for (int i = 0; i < numLines; i++) {
    lines[i] = new Line();
  }
}

void draw() {
  background(0);
  
  // 绘制每条直线
  for (int i = 0; i < numLines; i++) {
    lines[i].update();
    lines[i].display();
  }
}

// 直线类
class Line {
  float x;  // 起始x坐标
  float y;  // 起始y坐标
  float speed;  // 移动速度
  float length;  // 直线长度
  float angle;  // 移动角度
  float thickness;  // 线条粗细
  
  Line() {
    x = random(width);  // 随机生成起始x坐标
    y = random(height);  // 随机生成起始y坐标
    speed = random(1, 4);  // 随机生成移动速度
    length = dist(0, 0, width, height);  // 设置直线长度为画布对角线长度
    angle = random(TWO_PI);  // 随机生成移动角度
    thickness = random(1, 10);  // 随机生成线条粗细
  }
  
  void update() {
    // 更新直线的位置
    x += cos(angle) * speed;
    y += sin(angle) * speed;
    
    // 当直线移出画布时，重新设置起始位置和角度
    if (x > width + length || x < -length || y > height + length || y < -length) {
      x = random(width);
      y = random(height);
      angle = random(TWO_PI);
    }
  }
  
  void display() {
    // 绘制直线
    stroke(255);
    strokeWeight(thickness);
    line(x, y, x + cos(angle) * length, y + sin(angle) * length);
  }
}
