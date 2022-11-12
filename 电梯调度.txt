#include<stdio.h>
typedef struct dianti
{
    int ZT;//三种状态：静止，上行，下行
    int LX;//三种类型：双，单，全
    int cc;//此时停在的楼层数
    int DY;//此楼层是否被调用
    int SF;//是否有人用电梯
}SH;
SH a[4];
int SF, Ar, cc, gocc;
int k[3], m[3];
int Lookfor(int x, int y, int z)//计算楼层差值函数
{
    int t;
    if (a[x].ZT == 0)//此时a[x]电梯处于静止状态
    {
        if (y < z)
        {
            t= z - y;
        }
        else
        {
            t = y - z;
        }
    }    
    return t;
}
void main()
{
    //接人操作
	printf("     全部楼层     单层       双层     全部楼层             \n");
	printf("       (一)      （二）     （三）     （四）              \n");
    printf("       ____       ____       ____       ____               \n");
    printf("      $    $     $    $     $    $     $    $              \n");
    printf("        6          8          17         20                \n");
    printf("      $    $     $    $     $    $     $    $              \n");
    printf("       ^^^^       ^^^^       ^^^^       ^^^^               \n");
    a[0].ZT = 0;
    a[1].ZT = 0;
    a[2].ZT = 0;
    a[3].ZT = 0;
    a[0].cc = 6;
    a[1].cc= 8;//表示此时电梯停在的楼层数为7楼
    a[2].cc = 17;
    a[3].cc = 20;
    while (1)
    {
        a[0].LX = 2;//一号电梯所有楼层都停靠
        a[1].LX = 1;//二号电梯单号楼层都停靠
        a[2].LX = 0;//三号电梯双号楼层都停靠
        a[3].LX = 2;//四号电梯所有楼层都停靠
        int i;
        int SF1 = 0, j = 0;
        printf("----------------------------------------------\n");
        printf("若要用电梯请按按钮 1 ！\n");
        scanf("%d", &SF);//此时是否有人按电梯
        if (SF == 1)
        {
            printf("*****此时有用户按电梯！*****\n");
        }
        printf("用户所在楼层为: ");
        scanf("%d", &cc);//此时按电梯的人所在的楼层数
        printf("上楼请按 1 ，下楼请按 0: \n");
        scanf("%d", &Ar);//用户请求是上楼还是下楼标记
        printf("请选择要去的楼层: ");
        scanf("%d", &gocc);//用户要去的楼层
        if (SF == 1)//用户按电梯
        {
            if (Ar == 1)//用户要上楼
            {
                if (cc % 2 == 0)//用户所在为偶数楼层
                {
                    if (gocc % 2 == 1)//用户要去奇数楼层
                    {
                        for (i = 0; i < 4; i++)
                        {
                            if (a[i].LX == 2)
                            {
                                a[i].DY = 1;
                            }
                            else
                            {
                                a[i].DY = 0;
                            }
                            while (a[i].DY == 1)
                            {
                                k[SF1] = Lookfor(i, cc, a[i].cc);
                                m[SF1] = i;
                                SF1++;
                                a[i].DY = 0;
                            }
                        }
                        if (k[0] < k[1])
                        {
                            printf("离用户最近并且符合条件的电梯为：0\n");
                            a[0].cc = gocc;
                            a[0].ZT = 0;
                        }
                        else
                        {
                            printf("离用户最近并且符合条件的电梯为：3\n");
                            a[3].cc = gocc;
                            a[3].ZT = 0;
                        }
                    }
                    if (gocc % 2 == 0)//用户要去偶数楼层
                    {
                        for (i = 0; i < 4; i++)
                        {
                            if (a[i].LX == 2 || a[i].LX == 0)
                            {
                                a[i].DY = 1;
                            }
                            else
                            {
                                a[i].DY = 0;
                            }
                            while (a[i].DY == 1)
                            {
                                k[SF1] = Lookfor(i, cc, a[i].cc);
                                m[SF1] = i;
                                SF1++;
                                a[i].DY = 0;
                            }
                        }
                        if (k[0] < k[1])
                        {
                            if (k[0] < k[2])
                            {
                                printf("离用户最近并且符合条件的电梯为：0\n");
                                a[0].cc = gocc;
                                a[0].ZT = 0;
                            }
                            else
                            {
                                printf("离用户最近并且符合条件的电梯为：3\n");
                                a[3].cc = gocc;
                                a[3].ZT = 0;
                            }
                        }
                        else
                        {
                            if (k[1] < k[2])
                            {
                                printf("离用户最近并且符合条件的电梯为：2\n");
                                a[2].cc= gocc;
                                a[2].ZT = 0;
                            }
                            else
                            {
                                printf("离用户最近并且符合条件的电梯为：3\n");
                                a[3].cc = gocc;
                                a[3].ZT = 0;
                            }
                        }
                    }
                }
                if (cc% 2 == 1)//用户所在为奇数楼层
                {
                    if (gocc% 2 == 0)//用户要去偶数楼层
                    {
                        for (i = 0; i < 4; i++)
                        {
                            if (a[i].LX == 2)
                            {
                                a[i].DY = 1;
                            }
                            else
                            {
                                a[i].DY = 0;
                            }
                            while (a[i].DY == 1)
                            {
                                k[SF1] = Lookfor(i, cc, a[i].cc);
                                m[SF1] = i;
                                SF1++;
                                a[i].DY = 0;
                            }
                        }
                        if (k[0] < k[1])
                        {
                            printf("离用户最近并且符合条件的电梯为：0\n");
                            a[0].cc= gocc;
                            a[0].ZT = 0;
                        }
                        else
                        {
                            printf("离用户最近并且符合条件的电梯为：3\n");
                            a[3].cc= gocc;
                            a[3].ZT = 0;
                        }
                    }
                    if (gocc % 2 == 1)//用户要去奇数楼层
                    {
                        for (i = 0; i < 4; i++)
                        {
                            if (a[i].LX == 2 || a[i].LX == 1)
                            {
                                a[i].DY = 1;
                            }
                            else
                            {
                                a[i].DY = 0;
                            }
                            while (a[i].DY == 1)
                            {
                                k[SF1] = Lookfor(i, cc, a[i].cc);
                                m[SF1] = i;
                                SF1++;
                                a[i].DY = 0;
                            }
                        }
                        if (k[0] < k[1])
                        {
                            if (k[0] < k[2])
                            {
                                printf("离用户最近并且符合条件的电梯为：0\n");
                                a[0].cc = gocc;
                                a[0].ZT = 0;
                            }
                            else
                            {
                                printf("离用户最近并且符合条件的电梯为：3\n");
                                a[3].cc= gocc;
                                a[3].ZT = 0;
                            }
                        }
                        else
                        {
                            if (k[1] < k[2])
                            {
                                printf("离用户最近并且符合条件的电梯为：2\n");
                                a[1].cc = gocc;
                                a[1].ZT = 0;
                            }
                            else
                            {
                                printf("离用户最近并且符合条件的电梯为：3\n");
                                a[3].cc= gocc;
                                a[3].ZT = 0;
                            }
                        }
                    }
                }
            }
            if (Ar == 0)//用户要下楼
            {
                if (cc% 2 == 0)//用户所在为偶数楼层
                {
                    if (gocc% 2 == 1)//用户要去奇数楼层
                    {
                        for (i = 0; i < 4; i++)
                        {
                            if (a[i].LX == 2)
                            {
                                a[i].DY = 1;
                            }
                            else
                            {
                                a[i].DY = 0;
                            }
                            while (a[i].DY == 1)
                            {
                                k[SF1] = Lookfor(i, cc, a[i].cc);
                                m[SF1] = i;
                                SF1++;
                                a[i].DY = 0;
                            }
                        }
                        if (k[0] < k[1])
                        {
                            printf("离用户最近并且符合条件的电梯为：0\n");
                            a[0].cc= gocc;
                            a[0].ZT = 0;
                        }
                        else
                        {
                            printf("离用户最近并且符合条件的电梯为：3\n");
                            a[3].cc = gocc;
                            a[3].ZT = 0;
                        }
                    }
                    if (gocc% 2 == 0)//用户要去偶数楼层
                    {
                        for (i = 0; i < 4; i++)
                        {
                            if (a[i].LX == 2 || a[i].LX == 0)
                            {
                                a[i].DY = 1;
                            }
                            else
                            {
                                a[i].DY = 0;
                            }
                            while (a[i].DY == 1)
                            {
                                k[SF1] = Lookfor(i, cc, a[i].cc);
                                m[SF1] = i;
                                SF1++;
                                a[i].DY = 0;
                            }
                        }
                        if (k[0] < k[1])
                        {
                            if (k[0] < k[2])
                            {
                                printf("离用户最近并且符合条件的电梯为：0\n");
                                a[0].cc = gocc;
                                a[0].ZT = 0;
                            }
                            else
                            {
                                printf("离用户最近并且符合条件的电梯为：3\n");
                                a[3].cc= gocc;
                                a[3].ZT = 0;
                            }
                        }
                        else
                        {
                            if (k[1] < k[2])
                            {
                                printf("离用户最近并且符合条件的电梯为：2\n");
                                a[2].cc =gocc;
                                a[2].ZT = 0;
                            }
                            else
                            {
                                printf("离用户最近并且符合条件的电梯为：3\n");
                                a[3].cc = gocc;
                                a[3].ZT = 0;
                            }
                        }
                    }
                }
                if (cc % 2 == 1)//用户所在为奇数楼层
                {
                    if (gocc % 2 == 0)//用户要去偶数楼层
                    {
                        for (i = 0; i < 4; i++)
                        {
                            if (a[i].LX == 2)
                            {
                                a[i].DY = 1;
                            }
                            else
                            {
                                a[i].DY = 0;
                            }
                            while (a[i].DY == 1)
                            {
                                k[SF1] = Lookfor(i, cc, a[i].cc);
                                m[SF1] = i;
                                SF1++;
                                a[i].DY = 0;
                            }
                        }
                        if (k[0] < k[1])
                        {
                            printf("离用户最近并且符合条件的电梯为：0\n");
                            a[0].cc = gocc;
                            a[0].ZT = 0;
                        }
                        else
                        {
                            printf("离用户最近并且符合条件的电梯为：3\n");
                            a[3].cc = gocc;
                            a[3].ZT = 0;
                        }
                    }
                    if (gocc% 2 == 1)//用户要去奇数楼层
                    {
                        for (i = 0; i < 4; i++)
                        {
                            if (a[i].LX == 2 || a[i].LX == 1)
                            {
                                a[i].DY = 1;
                            }
                            else
                            {
                                a[i].DY = 0;
                            }
                            while (a[i].DY == 1)
                            {
                                k[SF1] = Lookfor(i, cc, a[i].cc);
                                m[SF1] = i;
                                SF1++;
                                a[i].DY = 0;
                            }
                        }
                        if (k[0] < k[1])
                        {
                            if (k[0] < k[2])
                            {
                                printf("离用户最近并且符合条件的电梯为：0\n");
                                a[0].cc= gocc;
                                a[0].ZT = 0;
                            }
                            else
                            {
                                printf("离用户最近并且符合条件的电梯为：3\n");
                                a[3].cc = gocc;
                                a[3].ZT = 0;
                            }
                        }
                        else
                        {
                            if (k[1] < k[2])
                            {
                                printf("离用户最近并且符合条件的电梯为：2\n");
                                a[1].cc= gocc;
                                a[1].ZT = 0;
                            }
                            else
                            {
                                printf("离用户最近并且符合条件的电梯为：3\n");
                                a[3].cc= gocc;
                                a[3].ZT = 0;
                            }
                        }
                    }
                }
            }
        }
        else if (SF == 0)
        {
            printf("此时无人用电梯");
        }
        printf("     全部楼层     单层       双层     全部楼层             \n");
	    printf("       (一)      （二）     （三）     （四）              \n");
        printf("       ____       ____       ____       ____               \n");
        printf("      $    $     $    $     $    $     $    $              \n");
        printf("        %d         %d         %d         %d                \n", a[0].cc, a[1].cc, a[2].cc, a[3].cc);
        printf("      $    $     $    $     $    $     $    $              \n");
        printf("       ^^^^       ^^^^       ^^^^       ^^^^               \n");
        printf("\n");
        printf("----------------------------------------------\n");
    }
}