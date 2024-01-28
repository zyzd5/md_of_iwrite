```matlab
log()   %表示自然对数ln()

linspace(num_start, num_end, num_count);
linspace(0, 2*pi, 101);

plot(x, y, '-')   %'-':直线, '--':虚线, ':':点形, '-.':虚线点
                  %'b':blue, 'r':red, 'k':black
bar(x, y, 'option')     %   条形图
stairs(x, y, 'option')  %   阶梯图
stem(x, y, 'option')    %   杆图
fill(x, y, 'option')    %   填充图
subplot(col, row, plot_num)     %指定大图中的子图像编号，加在最前面
title('title_string')   %需要加在生成图像语句的最后

%表示分段函数
x = -5:5    %range of x
y = (x>0).* x.^2 + (x<=0).* -(x.^2);    %expression of y    

%表示极坐标绘图
polarplot(theta, rho, 'option');

%曲面图绘图
[x, y] = meshgrid(x, y);    %提前处理x, y网格化
surf(x, y, z, 'option') %   曲面图
surfc(x, y, z, 'option')%   等高曲面图

%着色
shading %设置颜色着色属性。
shading faceted %具有叠加的黑色网格线的单一着色。这是默认的着色模式。
shading interp %对曲面或图形对象的颜色着色进行色彩的插值处理，使色彩平滑过渡。
shading flat %每个网格片用同一个颜色着色,网格线也是相应颜色

%科学计算
rand(row, col, num_type);      %0到1的随机数
mean(array);        %计算数组均值
std(array);         %计算数组标准差
%生成指定范围随机数
60 + (100-60) * rand(4, 5)      %生成60到100的随机数的4*5矩阵

fix()   //四舍五入数字
sort()  //从大到小排序
```