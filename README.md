## 内容

1. 可以选择`Math` 或` Chinese` 页面
2. `Math`页面下
   1. 可以选择运算的数值区间：小于10、小于20、小于50、小于100
   2. 可以选择计算题的题量：20题、50题、100题
   3. 可以选择几个数字的运算：2个、3个、4个
   4. 可以选择加减乘除算法
   5. 可以自动生成题目
   6. 可以显示题目答案
3. `Chinese`页面下
   1. 可以选择需要补全的古诗是前句还是后句
   2. 可以选择古诗题目的题量
   3. 可以自动生成古诗题目
   4. 可以显示题目答案

## 代码

### Math页面下的Generate Test的回调函数

```matlab
        function GenerateTestButtonPushed(app, event)
            global data1;
            global data2;
            
            %生成随机数存入data1中
            data1=zeros(str2num(app.QuantityDropDown.Value),str2num(app.NumbersDropDown.Value));
            for countquan = 1:str2num(app.QuantityDropDown.Value)
                for countnumb = 1:str2num(app.NumbersDropDown.Value)
                    data1(countquan,countnumb) = randi([1 str2num(app.DifficultyDropDown.Value)],1,1);
                end
            end
            
            %判断复选框的勾选情况，启用不同的四则运算算法（+,-,*,/）
            data2=zeros(str2num(app.QuantityDropDown.Value),str2num(app.NumbersDropDown.Value)-1);
            for countquan = 1:str2num(app.QuantityDropDown.Value)
                for countnumb = 1:str2num(app.NumbersDropDown.Value)-1
                    if (app.CheckBox.Value == 1 && app.CheckBox_2.Value == 0 && app.CheckBox_2.Value == 0 && app.CheckBox_3.Value == 0)
                        data2(countquan,countnumb) = randi([1 1],1,1);
                    elseif (app.CheckBox.Value == 1 && app.CheckBox_2.Value == 1 && app.CheckBox_3.Value == 0 && app.CheckBox_4.Value == 0)
                        data2(countquan,countnumb) = randi([1 2],1,1);
                    elseif (app.CheckBox.Value == 1 && app.CheckBox_2.Value == 1 && app.CheckBox_3.Value == 1 && app.CheckBox_4.Value == 0)
                        data2(countquan,countnumb) = randi([1 3],1,1);
                    elseif (app.CheckBox.Value == 1 && app.CheckBox_2.Value == 1 && app.CheckBox_3.Value == 1 && app.CheckBox_4.Value == 1)
                        data2(countquan,countnumb) = randi([1 4],1,1);
                    end
                end
            end
             
             %将四则运算算法用文字表示，并将数字和符号存入table中
             if (str2num(app.NumbersDropDown.Value) == 2) %如果需要运算的数字有2个，则按如下操作
                T(:,1) = table(data1(:,1));
                for countquan = 1:str2num(app.QuantityDropDown.Value)
                        if (data2(countquan,1) == 1)
                            T(countquan,2) = {"+"};
                        elseif (data2(countquan,1) == 2)
                            T(countquan,2) = {"-"};
                        elseif (data2(countquan,1) == 3)
                            T(countquan,2) = {"×"};
                        elseif (data2(countquan,1) == 4)
                            T(countquan,2) = {"÷"};
                        end
                end
                 T(:,3) = table(data1(:,2));
                 T(:,4) = {"="};
            elseif (str2num(app.NumbersDropDown.Value) == 3)%如果需要运算的数字有3个，则按如下操作
                T(:,1) = table(data1(:,1));
                for countquan = 1:str2num(app.QuantityDropDown.Value)
                        if (data2(countquan,1) == 1)
                            T(countquan,2) = {"+"};
                        elseif (data2(countquan,1) == 2)
                            T(countquan,2) = {"-"};
                        elseif (data2(countquan,1) == 3)
                            T(countquan,2) = {"×"};
                        elseif (data2(countquan,1) == 4)
                            T(countquan,2) = {"÷"};
                        end
                end               
                T(:,3) = table(data1(:,2));
                for countquan = 1:str2num(app.QuantityDropDown.Value)
                        if (data2(countquan,2) == 1)
                            T(countquan,4) = {"+"};
                        elseif (data2(countquan,2) == 2)
                            T(countquan,4) = {"-"};
                        elseif (data2(countquan,2) == 3)
                            T(countquan,4) = {"×"};
                        elseif (data2(countquan,2) == 4)
                            T(countquan,4) = {"÷"};
                        end
                end
                T(:,5) = table(data1(:,3));
                T(:,6) = {"="};
            elseif (str2num(app.NumbersDropDown.Value) == 4)%如果需要运算的数字有4个，则按如下操作
                T(:,1) = table(data1(:,1));
                for countquan = 1:str2num(app.QuantityDropDown.Value)
                        if (data2(countquan,1) == 1)
                            T(countquan,2) = {"+"};
                        elseif (data2(countquan,1) == 2)
                            T(countquan,2) = {"-"};
                        elseif (data2(countquan,1) == 3)
                            T(countquan,2) = {"×"};
                        elseif (data2(countquan,1) == 4)
                            T(countquan,2) = {"÷"};
                        end
                end
                T(:,3) = table(data1(:,2));
                for countquan = 1:str2num(app.QuantityDropDown.Value)
                        if (data2(countquan,2) == 1)
                            T(countquan,4) = {"+"};
                        elseif (data2(countquan,2) == 2)
                            T(countquan,4) = {"-"};
                        elseif (data2(countquan,2) == 3)
                            T(countquan,4) = {"×"};
                        elseif (data2(countquan,2) == 4)
                            T(countquan,4) = {"÷"};
                        end
                end
                T(:,5) = table(data1(:,3));
                for countquan = 1:str2num(app.QuantityDropDown.Value)
                        if (data2(countquan,3) == 1)
                            T(countquan,6) = {"+"};
                        elseif (data2(countquan,3) == 2)
                            T(countquan,6) = {"-"};
                        elseif (data2(countquan,3) == 3)
                            T(countquan,6) = {"×"};
                        elseif (data2(countquan,3) == 4)
                            T(countquan,6) = {"÷"};
                        end
                end
                T(:,7) = table(data1(:,4)); 
                T(:,8) = {"="};
             end
            
            %把变量存入工作区，调试用
            assignin('base','T',T);
            assignin('base','data1',data1);
            assignin('base','data2',data2);

            %将table存入GenerateTest.txt中
            writetable(T,'GenerateTest.txt','Delimiter',' ');
            %通过notepad程序将GenerateTest.txt文本打开
            !start notepad.exe GenerateTest.txt
        end
```

### Math页面下的Show Answer的回调函数

```matlab
		function ShowAnswerButtonPushed(app, event)
            global data1;
            global data2;
            data3 = strings(str2num(app.QuantityDropDown.Value),str2num(app.QuantityDropDown.Value)-1);
            data4 = strings(str2num(app.QuantityDropDown.Value),1);
            for countquan = 1:str2num(app.QuantityDropDown.Value)%将复选框选中的四则运算算法用标准写法替换
                for countnumb = 1:str2num(app.NumbersDropDown.Value)-1
                        if (data2(countquan,countnumb) == 1)
                            data3(countquan,countnumb) = '+';
                        elseif (data2(countquan,countnumb) == 2)
                            data3(countquan,countnumb) = '-';
                        elseif (data2(countquan,countnumb) == 3)
                            data3(countquan,countnumb) = '*';
                        elseif (data2(countquan,countnumb) == 4)
                            data3(countquan,countnumb) = '/';
                        end
                end
            end
            
            sp = {32};%空格符，使输出整齐美观
            
            %在不同计算个数的情况下，将数字和符号合并为字符串，为计算提供方便
            if (str2num(app.NumbersDropDown.Value) == 2)
                for countquan = 1:str2num(app.QuantityDropDown.Value)
                    data4(countquan) = strcat(int2str(data1(countquan,1)),sp,data3(countquan,1),sp,int2str(data1(countquan,2))); 
                end
            elseif (str2num(app.NumbersDropDown.Value) == 3)
                for countquan = 1:str2num(app.QuantityDropDown.Value)
                    data4(countquan) = strcat(int2str(data1(countquan,1)),sp,data3(countquan,1),sp,int2str(data1(countquan,2)),sp,data3(countquan,2),sp,int2str(data1(countquan,3))); 
                end
            elseif (str2num(app.NumbersDropDown.Value) == 4)
                for countquan = 1:str2num(app.QuantityDropDown.Value)
                    data4(countquan) = strcat(int2str(data1(countquan,1)),sp,data3(countquan,1),sp,int2str(data1(countquan,2)),sp,data3(countquan,2),sp,int2str(data1(countquan,3)),sp,data3(countquan,3),sp,int2str(data1(countquan,4))); 
                end
            end
            
            for countquan = 1:str2num(app.QuantityDropDown.Value)
                data4(countquan) = strcat(data4(countquan),sp,'=',sp,num2str(eval(data4(countquan))));
                %使用eval函数对字符串进行计算
            end
            %调试用
            assignin('base','data3',data3);
            assignin('base','data4',data4);
            %将计算结果保存到ShowAnswer.txt中，并通过notepad程序自动打开
            answer = fopen('ShowAnswer.txt','w+');
            fprintf(answer,'%s\n',data4);
            fclose(answer);
            !start notepad.exe ShowAnswer.txt

        end
```

### Chinese页面下的Generate Test的回调函数

```matlab
        function GenerateTestButton_2Pushed(app, event)
            global randlist;
            load chinese.mat;%将chinese.mat的数据导入进matlab
            randlist =  randperm(str2num(app.QuantityDropDown_2.Value));%将题号打乱
            gushi = strings(str2num(app.QuantityDropDown_2.Value),1);
            
            %根据Difficulty中的设置，选择需要填的是前句还是后句
            if (app.DifficultyDropDown_2.Value == '1')
                for countquan = 1:str2num(app.QuantityDropDown_2.Value)
                    gushi(countquan,1) = strcat('-------------- , ',chinese(randlist(1,countquan),2));   
                end
            elseif (app.DifficultyDropDown_2.Value == '2')
                for countquan = 1:str2num(app.QuantityDropDown_2.Value)
                    gushi(countquan,1) = strcat(chinese(randlist(1,countquan),1),' , --------------');
                end
            elseif (app.DifficultyDropDown_2.Value == '3')
                for countquan = 1:str2num(app.QuantityDropDown_2.Value)/2
                    gushi(countquan*2-1,1) = strcat(chinese(randlist(1,countquan*2-1),1),' , -------------');
                    gushi(countquan*2,1) = strcat('-------------- , ',chinese(randlist(1,countquan*2),2)); 
                end
            end
            
            %调试用
            assignin('base','randlist',randlist);
            assignin('base','gushi',gushi);
            
            %将生成的题目保存到Chinese.txt中，并用notepad程序自动打开
            test = fopen('Chinese.txt','w+');
            fprintf(test,'%s\n',gushi);
            fclose(test);
            !start notepad.exe Chinese.txt
        end
```

### Chinese页面下的Show Answer的回调函数

```matlab
		function ShowAnswerButton_2Pushed(app, event)
            global randlist;
            load chinese.mat%导入chinese.mat
            
            %生成答案
            for countquan = 1:str2num(app.QuantityDropDown_2.Value)
                    gushi(countquan,1) = strcat(chinese(randlist(1,countquan),1),',',chinese(randlist(1,countquan),2));   
            end
            
            %将答案保存为ChineseAnswer.txt，并通过notepad打开
            answer = fopen('ChineseAnswer.txt','w+');
            fprintf(answer,'%s\n',gushi);
            fclose(answer);
            !start notepad.exe ChineseAnswer.txt
        end
```



## 运行结果

启动的初始界面如下：

![Snipaste_2020-04-03_18-36-57](img\Snipaste_2020-04-03_18-36-57.png)

默认是10以内的数字，20个题目，两个数字相加，点击`Generate Test`按钮，弹出题目记事本：

![Snipaste_2020-04-03_18-38-37](img\Snipaste_2020-04-03_18-38-37.png)

点击Show Answer按钮，则弹出计算题目答案的记事本：

![Snipaste_2020-04-03_18-39-06](img\Snipaste_2020-04-03_18-39-06.png)

将`Difficulty`改为100以内的数字：

![Snipaste_2020-04-03_18-39-35](\img\Snipaste_2020-04-03_18-39-35.png)

将`Quantity`改为100道题目：

![Snipaste_2020-04-03_18-39-43](\img\Snipaste_2020-04-03_18-39-43.png)

将`Numbers`改为4个数字进行运算：

![Snipaste_2020-04-03_18-39-53](\img\Snipaste_2020-04-03_18-39-53.png)

启用加减乘除四则运算：

![Snipaste_2020-04-03_18-40-03](\img\Snipaste_2020-04-03_18-40-03.png)

点击`Generate Test`按钮，弹出计算题的记事本：

![Snipaste_2020-04-03_18-40-18](\img\Snipaste_2020-04-03_18-40-18.png)

点击`Show Answer`按钮，弹出计算题答案的记事本：

![Snipaste_2020-04-03_18-40-32](\img\Snipaste_2020-04-03_18-40-32.png)

点击`Chinese`标签，进行古诗题目操作：

![Snipaste_2020-04-03_18-40-47](\img\Snipaste_2020-04-03_18-40-47.png)

初始设置是给出后句，填上句，共四个题目，点击`GenerateTest`按钮，弹出题目记事本：

![Snipaste_2020-04-03_18-41-07](\img\Snipaste_2020-04-03_18-41-07.png)

点击`ShowAnswer`按钮，弹出题目答案记事本：

![Snipaste_2020-04-03_18-41-25](\img\Snipaste_2020-04-03_18-41-25.png)

选择`Difficulty`为`right`，提示上句，填下句：

![Snipaste_2020-04-03_18-41-48](\img\Snipaste_2020-04-03_18-41-48.png)

选择`Quantity`为30，题量为30题：

![Snipaste_2020-04-03_18-42-00](\img\Snipaste_2020-04-03_18-42-00.png)

点击`GenerateTest`按钮，弹出题目记事本：

![Snipaste_2020-04-03_18-42-11](\img\Snipaste_2020-04-03_18-42-11.png)

点击`ShowAnswer`按钮，弹出题目答案记事本：

![Snipaste_2020-04-03_18-42-29](\img\Snipaste_2020-04-03_18-42-29.png)

选择`Difficulty`为mix，随机显示前句写后句或显示后句写前句：

![Snipaste_2020-04-03_18-42-39](\img\Snipaste_2020-04-03_18-42-39.png)

选择`Quantity`为50，题量为50题：

![Snipaste_2020-04-03_18-42-46](\img\Snipaste_2020-04-03_18-42-46.png)

点击`GenerateTest`按钮，弹出题目记事本：

![Snipaste_2020-04-03_18-42-59](\img\Snipaste_2020-04-03_18-42-59.png)

点击`ShowAnswer`按钮，弹出题目答案记事本：

![Snipaste_2020-04-03_18-43-11](\img\Snipaste_2020-04-03_18-43-11.png)

## 其它

### 完整代码

```matlab
classdef app1 < matlab.apps.AppBase

    % Properties that correspond to app components
    properties (Access = public)
        app1UIFigure               matlab.ui.Figure
        TabGroup                   matlab.ui.container.TabGroup
        MathTab                    matlab.ui.container.Tab
        GenerateTestButton         matlab.ui.control.Button
        ShowAnswerButton           matlab.ui.control.Button
        CheckBox                   matlab.ui.control.CheckBox
        CheckBox_2                 matlab.ui.control.CheckBox
        CheckBox_3                 matlab.ui.control.CheckBox
        CheckBox_4                 matlab.ui.control.CheckBox
        DifficultyLabel            matlab.ui.control.Label
        DifficultyDropDown         matlab.ui.control.DropDown
        QuantityDropDownLabel      matlab.ui.control.Label
        QuantityDropDown           matlab.ui.control.DropDown
        NumbersDropDownLabel       matlab.ui.control.Label
        NumbersDropDown            matlab.ui.control.DropDown
        ChineseTab                 matlab.ui.container.Tab
        DifficultyDropDown_2Label  matlab.ui.control.Label
        DifficultyDropDown_2       matlab.ui.control.DropDown
        QuantityDropDown_2Label    matlab.ui.control.Label
        QuantityDropDown_2         matlab.ui.control.DropDown
        GenerateTestButton_2       matlab.ui.control.Button
        ShowAnswerButton_2         matlab.ui.control.Button
    end



    methods (Access = private)

        % Button pushed function: GenerateTestButton
        function GenerateTestButtonPushed(app, event)
            global data1;
            global data2;
            

            data1=zeros(str2num(app.QuantityDropDown.Value),str2num(app.NumbersDropDown.Value));
            for countquan = 1:str2num(app.QuantityDropDown.Value)
                for countnumb = 1:str2num(app.NumbersDropDown.Value)
                    data1(countquan,countnumb) = randi([1 str2num(app.DifficultyDropDown.Value)],1,1);
                end
            end
            
            
            data2=zeros(str2num(app.QuantityDropDown.Value),str2num(app.NumbersDropDown.Value)-1);
            for countquan = 1:str2num(app.QuantityDropDown.Value)
                for countnumb = 1:str2num(app.NumbersDropDown.Value)-1
                    if (app.CheckBox.Value == 1 && app.CheckBox_2.Value == 0 && app.CheckBox_2.Value == 0 && app.CheckBox_3.Value == 0)
                        data2(countquan,countnumb) = randi([1 1],1,1);
                    elseif (app.CheckBox.Value == 1 && app.CheckBox_2.Value == 1 && app.CheckBox_3.Value == 0 && app.CheckBox_4.Value == 0)
                        data2(countquan,countnumb) = randi([1 2],1,1);
                    elseif (app.CheckBox.Value == 1 && app.CheckBox_2.Value == 1 && app.CheckBox_3.Value == 1 && app.CheckBox_4.Value == 0)
                        data2(countquan,countnumb) = randi([1 3],1,1);
                    elseif (app.CheckBox.Value == 1 && app.CheckBox_2.Value == 1 && app.CheckBox_3.Value == 1 && app.CheckBox_4.Value == 1)
                        data2(countquan,countnumb) = randi([1 4],1,1);
                    end
                end
            end
                        
             if (str2num(app.NumbersDropDown.Value) == 2)
                T(:,1) = table(data1(:,1));
                for countquan = 1:str2num(app.QuantityDropDown.Value)
                        if (data2(countquan,1) == 1)
                            T(countquan,2) = {"+"};
                        elseif (data2(countquan,1) == 2)
                            T(countquan,2) = {"-"};
                        elseif (data2(countquan,1) == 3)
                            T(countquan,2) = {"×"};
                        elseif (data2(countquan,1) == 4)
                            T(countquan,2) = {"÷"};
                        end
                end
                 T(:,3) = table(data1(:,2));
                 T(:,4) = {"="};
            elseif (str2num(app.NumbersDropDown.Value) == 3)
                T(:,1) = table(data1(:,1));
                for countquan = 1:str2num(app.QuantityDropDown.Value)
                        if (data2(countquan,1) == 1)
                            T(countquan,2) = {"+"};
                        elseif (data2(countquan,1) == 2)
                            T(countquan,2) = {"-"};
                        elseif (data2(countquan,1) == 3)
                            T(countquan,2) = {"×"};
                        elseif (data2(countquan,1) == 4)
                            T(countquan,2) = {"÷"};
                        end
                end               
                T(:,3) = table(data1(:,2));
                for countquan = 1:str2num(app.QuantityDropDown.Value)
                        if (data2(countquan,2) == 1)
                            T(countquan,4) = {"+"};
                        elseif (data2(countquan,2) == 2)
                            T(countquan,4) = {"-"};
                        elseif (data2(countquan,2) == 3)
                            T(countquan,4) = {"×"};
                        elseif (data2(countquan,2) == 4)
                            T(countquan,4) = {"÷"};
                        end
                end
                T(:,5) = table(data1(:,3));
                T(:,6) = {"="};
            elseif (str2num(app.NumbersDropDown.Value) == 4)
                T(:,1) = table(data1(:,1));
                for countquan = 1:str2num(app.QuantityDropDown.Value)
                        if (data2(countquan,1) == 1)
                            T(countquan,2) = {"+"};
                        elseif (data2(countquan,1) == 2)
                            T(countquan,2) = {"-"};
                        elseif (data2(countquan,1) == 3)
                            T(countquan,2) = {"×"};
                        elseif (data2(countquan,1) == 4)
                            T(countquan,2) = {"÷"};
                        end
                end
                T(:,3) = table(data1(:,2));
                for countquan = 1:str2num(app.QuantityDropDown.Value)
                        if (data2(countquan,2) == 1)
                            T(countquan,4) = {"+"};
                        elseif (data2(countquan,2) == 2)
                            T(countquan,4) = {"-"};
                        elseif (data2(countquan,2) == 3)
                            T(countquan,4) = {"×"};
                        elseif (data2(countquan,2) == 4)
                            T(countquan,4) = {"÷"};
                        end
                end
                T(:,5) = table(data1(:,3));
                for countquan = 1:str2num(app.QuantityDropDown.Value)
                        if (data2(countquan,3) == 1)
                            T(countquan,6) = {"+"};
                        elseif (data2(countquan,3) == 2)
                            T(countquan,6) = {"-"};
                        elseif (data2(countquan,3) == 3)
                            T(countquan,6) = {"×"};
                        elseif (data2(countquan,3) == 4)
                            T(countquan,6) = {"÷"};
                        end
                end
                T(:,7) = table(data1(:,4)); 
                T(:,8) = {"="};
             end
            
            assignin('base','T',T);
            assignin('base','data1',data1);
            assignin('base','data2',data2);


            writetable(T,'GenerateTest.txt','Delimiter',' ');

            !start notepad.exe GenerateTest.txt


        end

        % Button pushed function: ShowAnswerButton
        function ShowAnswerButtonPushed(app, event)
            global data1;
            global data2;
            data3 = strings(str2num(app.QuantityDropDown.Value),str2num(app.QuantityDropDown.Value)-1);
            data4 = strings(str2num(app.QuantityDropDown.Value),1);
            for countquan = 1:str2num(app.QuantityDropDown.Value)
                for countnumb = 1:str2num(app.NumbersDropDown.Value)-1
                        if (data2(countquan,countnumb) == 1)
                            data3(countquan,countnumb) = '+';
                        elseif (data2(countquan,countnumb) == 2)
                            data3(countquan,countnumb) = '-';
                        elseif (data2(countquan,countnumb) == 3)
                            data3(countquan,countnumb) = '*';
                        elseif (data2(countquan,countnumb) == 4)
                            data3(countquan,countnumb) = '/';
                        end
                end
            end
            
            sp = {32};
            
            if (str2num(app.NumbersDropDown.Value) == 2)
                for countquan = 1:str2num(app.QuantityDropDown.Value)
                    data4(countquan) = strcat(int2str(data1(countquan,1)),sp,data3(countquan,1),sp,int2str(data1(countquan,2))); 
                end
            elseif (str2num(app.NumbersDropDown.Value) == 3)
                for countquan = 1:str2num(app.QuantityDropDown.Value)
                    data4(countquan) = strcat(int2str(data1(countquan,1)),sp,data3(countquan,1),sp,int2str(data1(countquan,2)),sp,data3(countquan,2),sp,int2str(data1(countquan,3))); 
                end
            elseif (str2num(app.NumbersDropDown.Value) == 4)
                for countquan = 1:str2num(app.QuantityDropDown.Value)
                    data4(countquan) = strcat(int2str(data1(countquan,1)),sp,data3(countquan,1),sp,int2str(data1(countquan,2)),sp,data3(countquan,2),sp,int2str(data1(countquan,3)),sp,data3(countquan,3),sp,int2str(data1(countquan,4))); 
                end
            end
            
            for countquan = 1:str2num(app.QuantityDropDown.Value)
                data4(countquan) = strcat(data4(countquan),sp,'=',sp,num2str(eval(data4(countquan))));
            end
            assignin('base','data3',data3);
            assignin('base','data4',data4);
            answer = fopen('ShowAnswer.txt','w+');
            fprintf(answer,'%s\n',data4);
            fclose(answer);
            !start notepad.exe ShowAnswer.txt

        end

        % Button pushed function: GenerateTestButton_2
        function GenerateTestButton_2Pushed(app, event)
            global randlist;
            load chinese.mat;
            randlist =  randperm(str2num(app.QuantityDropDown_2.Value));
            gushi = strings(str2num(app.QuantityDropDown_2.Value),1);
            
            if (app.DifficultyDropDown_2.Value == '1')
                for countquan = 1:str2num(app.QuantityDropDown_2.Value)
                    gushi(countquan,1) = strcat('-------------- , ',chinese(randlist(1,countquan),2));   
                end
            elseif (app.DifficultyDropDown_2.Value == '2')
                for countquan = 1:str2num(app.QuantityDropDown_2.Value)
                    gushi(countquan,1) = strcat(chinese(randlist(1,countquan),1),' , --------------');
                end
            elseif (app.DifficultyDropDown_2.Value == '3')
                for countquan = 1:str2num(app.QuantityDropDown_2.Value)/2
                    gushi(countquan*2-1,1) = strcat(chinese(randlist(1,countquan*2-1),1),' , -------------');
                    gushi(countquan*2,1) = strcat('-------------- , ',chinese(randlist(1,countquan*2),2)); 
                end
            end
            assignin('base','randlist',randlist);
            assignin('base','gushi',gushi);
            test = fopen('Chinese.txt','w+');
            fprintf(test,'%s\n',gushi);
            fclose(test);
            !start notepad.exe Chinese.txt
        end

        % Button pushed function: ShowAnswerButton_2
        function ShowAnswerButton_2Pushed(app, event)
            global randlist;
            load chinese.mat
            for countquan = 1:str2num(app.QuantityDropDown_2.Value)
                    gushi(countquan,1) = strcat(chinese(randlist(1,countquan),1),',',chinese(randlist(1,countquan),2));   
            end
            answer = fopen('ChineseAnswer.txt','w+');
            fprintf(answer,'%s\n',gushi);
            fclose(answer);
            !start notepad.exe ChineseAnswer.txt
        end
    end

    % App initialization and construction
    methods (Access = private)

        % Create UIFigure and components
        function createComponents(app)

            % Create app1UIFigure
            app.app1UIFigure = uifigure;
            app.app1UIFigure.Position = [100 100 395 145];
            app.app1UIFigure.Name = 'app1';

            % Create TabGroup
            app.TabGroup = uitabgroup(app.app1UIFigure);
            app.TabGroup.Position = [1 -6 403 152];

            % Create MathTab
            app.MathTab = uitab(app.TabGroup);
            app.MathTab.Title = 'Math';
            app.MathTab.BackgroundColor = [1 1 1];

            % Create GenerateTestButton
            app.GenerateTestButton = uibutton(app.MathTab, 'push');
            app.GenerateTestButton.ButtonPushedFcn = createCallbackFcn(app, @GenerateTestButtonPushed, true);
            app.GenerateTestButton.Position = [67 22 100 22];
            app.GenerateTestButton.Text = 'Generate Test';

            % Create ShowAnswerButton
            app.ShowAnswerButton = uibutton(app.MathTab, 'push');
            app.ShowAnswerButton.ButtonPushedFcn = createCallbackFcn(app, @ShowAnswerButtonPushed, true);
            app.ShowAnswerButton.Position = [258 22 100 22];
            app.ShowAnswerButton.Text = 'Show Answer';

            % Create CheckBox
            app.CheckBox = uicheckbox(app.MathTab);
            app.CheckBox.Text = '+';
            app.CheckBox.Position = [235 52 29 22];
            app.CheckBox.Value = true;

            % Create CheckBox_2
            app.CheckBox_2 = uicheckbox(app.MathTab);
            app.CheckBox_2.Text = '-';
            app.CheckBox_2.Position = [274 52 26 22];

            % Create CheckBox_3
            app.CheckBox_3 = uicheckbox(app.MathTab);
            app.CheckBox_3.Text = '×';
            app.CheckBox_3.Position = [309 52 29 22];

            % Create CheckBox_4
            app.CheckBox_4 = uicheckbox(app.MathTab);
            app.CheckBox_4.Text = '÷';
            app.CheckBox_4.Position = [348 52 29 22];

            % Create DifficultyLabel
            app.DifficultyLabel = uilabel(app.MathTab);
            app.DifficultyLabel.HorizontalAlignment = 'right';
            app.DifficultyLabel.Position = [34 85 51 22];
            app.DifficultyLabel.Text = 'Difficulty';

            % Create DifficultyDropDown
            app.DifficultyDropDown = uidropdown(app.MathTab);
            app.DifficultyDropDown.Items = {'10', '20', '50', '100'};
            app.DifficultyDropDown.Position = [103 85 100 22];
            app.DifficultyDropDown.Value = '10';

            % Create QuantityDropDownLabel
            app.QuantityDropDownLabel = uilabel(app.MathTab);
            app.QuantityDropDownLabel.HorizontalAlignment = 'right';
            app.QuantityDropDownLabel.Position = [225 85 50 22];
            app.QuantityDropDownLabel.Text = 'Quantity';

            % Create QuantityDropDown
            app.QuantityDropDown = uidropdown(app.MathTab);
            app.QuantityDropDown.Items = {'20', '50', '100'};
            app.QuantityDropDown.Position = [290 85 100 22];
            app.QuantityDropDown.Value = '20';

            % Create NumbersDropDownLabel
            app.NumbersDropDownLabel = uilabel(app.MathTab);
            app.NumbersDropDownLabel.HorizontalAlignment = 'right';
            app.NumbersDropDownLabel.Position = [34 52 54 22];
            app.NumbersDropDownLabel.Text = 'Numbers';

            % Create NumbersDropDown
            app.NumbersDropDown = uidropdown(app.MathTab);
            app.NumbersDropDown.Items = {'2', '3', '4'};
            app.NumbersDropDown.Position = [103 52 100 22];
            app.NumbersDropDown.Value = '2';

            % Create ChineseTab
            app.ChineseTab = uitab(app.TabGroup);
            app.ChineseTab.Title = 'Chinese';
            app.ChineseTab.BackgroundColor = [1 1 1];

            % Create DifficultyDropDown_2Label
            app.DifficultyDropDown_2Label = uilabel(app.ChineseTab);
            app.DifficultyDropDown_2Label.HorizontalAlignment = 'right';
            app.DifficultyDropDown_2Label.Position = [26 81 51 22];
            app.DifficultyDropDown_2Label.Text = 'Difficulty';

            % Create DifficultyDropDown_2
            app.DifficultyDropDown_2 = uidropdown(app.ChineseTab);
            app.DifficultyDropDown_2.Items = {'left', 'right', 'mix'};
            app.DifficultyDropDown_2.ItemsData = {'1', '2', '3'};
            app.DifficultyDropDown_2.Position = [92 81 100 22];
            app.DifficultyDropDown_2.Value = '1';

            % Create QuantityDropDown_2Label
            app.QuantityDropDown_2Label = uilabel(app.ChineseTab);
            app.QuantityDropDown_2Label.HorizontalAlignment = 'right';
            app.QuantityDropDown_2Label.Position = [219 81 50 22];
            app.QuantityDropDown_2Label.Text = 'Quantity';

            % Create QuantityDropDown_2
            app.QuantityDropDown_2 = uidropdown(app.ChineseTab);
            app.QuantityDropDown_2.Items = {'10', '30', '50'};
            app.QuantityDropDown_2.Position = [284 81 100 22];
            app.QuantityDropDown_2.Value = '10';

            % Create GenerateTestButton_2
            app.GenerateTestButton_2 = uibutton(app.ChineseTab, 'push');
            app.GenerateTestButton_2.ButtonPushedFcn = createCallbackFcn(app, @GenerateTestButton_2Pushed, true);
            app.GenerateTestButton_2.Position = [76 28 100 22];
            app.GenerateTestButton_2.Text = 'GenerateTest';

            % Create ShowAnswerButton_2
            app.ShowAnswerButton_2 = uibutton(app.ChineseTab, 'push');
            app.ShowAnswerButton_2.ButtonPushedFcn = createCallbackFcn(app, @ShowAnswerButton_2Pushed, true);
            app.ShowAnswerButton_2.Position = [252 28 100 22];
            app.ShowAnswerButton_2.Text = 'ShowAnswer';
        end
    end

    methods (Access = public)

        % Construct app
        function app = app1

            % Create and configure components
            createComponents(app)

            % Register the app with App Designer
            registerApp(app, app.app1UIFigure)

            if nargout == 0
                clear app
            end
        end

        % Code that executes before app deletion
        function delete(app)

            % Delete UIFigure when app is deleted
            delete(app.app1UIFigure)
        end
    end
end
```

### chinese.mat文件内容

| **春眠不觉晓** | **处处闻啼鸟** |
| :------------: | :------------: |
| **夜来风雨声** | **花落知多少** |
| **空山不见人** | **但闻人语响** |
| **返影入深林** | **复照青苔上** |
| **红豆生南国** | **春来发几枝** |
| **愿君多采撷** | **此物最相思** |
| **君自故乡来** | **应知故乡事** |
| **来日绮窗前** | **寒梅著花未** |
| **终南阴岭秀** | **积雪浮云端** |
| **林表明霁色** | **城中增暮寒** |
| **床前明月光** | **疑是地上霜** |
| **举头望明月** | **低头思故乡** |
| **白日依山尽** | **黄河入海流** |
| **欲穷千里目** | **更上一层楼** |
| **千山鸟飞绝** | **万径人踪灭** |
| **孤舟蓑笠翁** | **独钓寒江雪** |
| **向晚意不适** | **驱车登古原** |
| **夕阳无限好** | **只是近黄昏** |
| **泠泠七弦上** | **静听松风寒** |
| **古调虽自爱** | **今人多不弹** |
| **功盖三分国** | **名成八阵图** |
| **江流石不转** | **遣恨失吞吴** |
| **离离原上草** | **一岁一枯荣** |
| **野火烧不尽** | **春风吹又生** |
| **远芳侵古道** | **晴翠接荒城** |
| **又送王孙去** | **萋萋满别情** |
| **慈母手中线** | **游子身上衣** |
| **临行密密缝** | **意恐迟迟归** |
| **谁言寸草心** | **报得三春晖** |
| **明月出天山** | **苍茫云海间** |
| **长风几万里** | **吹度玉门关** |
| **汉下白登道** | **胡窥青海湾** |
| **由来征战地** | **不见有人还** |
| **戍客望边色** | **思归多苦颜** |
| **高楼当此夜** | **叹息未应闲** |
| **海上生明月** | **天涯共此时** |
| **情人怨遥夜** | **竟夕起相思** |
| **灭烛怜光满** | **披衣觉露滋** |
| **不堪盈手赠** | **还寝梦佳期** |
| **城阙辅三秦** | **风烟望五津** |
| **与君离别意** | **同是宦游人** |
| **海内存知己** | **天涯若比邻** |
| **无为在岐路** | **儿女共沾巾** |
| **国破山河在** | **城春草木深** |
| **感时花溅泪** | **恨别鸟惊心** |
| **烽火连三月** | **家书抵万金** |
| **白头搔更短** | **浑欲不胜簪** |
| **昔闻洞庭水** | **今上岳阳楼** |
| **吴楚东南坼** | **乾坤日夜浮** |
| **亲朋无一字** | **老病有孤舟** |
| **戎马关山北** | **凭轩涕泗流** |
| **中岁颇好道** | **晚家南山陲** |
| **兴来每独往** | **胜事空自知** |
| **行到水穷处** | **坐看云起时** |
| **偶然值林叟** | **谈笑无还期** |
| **春眠不觉晓** | **处处闻啼鸟** |
| **夜来风雨声** | **花落知多少** |
| **空山不见人** | **但闻人语响** |
| **返景入深林** | **复照青苔上** |
| **白日依山尽** | **黄河入海流** |
| **欲穷千里目** | **更上一层楼** |
