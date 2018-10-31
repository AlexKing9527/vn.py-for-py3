# vn.py - By Traders, For Traders.

目的：在 vn.py 基础上增加在py3上的适用性和一些自定义模块

  Successful Api: CTP、Olando 
  
Quick Start
    在SimNow注册CTP仿真账号，记下你的账号、密码、经纪商编号，然后下载快期查询你的交易和行情服务器地址

    找到vn.py应用示例目录examples，打开examples\VnTrader\CTP_connect.json，修改账号、密码、服务器等为上一步注册完成后你的信息（注意使用专门的编程编辑器，如Sublime Text等，防止json编码出错）

    找到VnTrader的启动入口run.py，并双击运行（若无法双击，则在当前目录按住Shift点鼠标右键，打开cmd输入python run.py运行），run.py内容如下：

    # encoding: UTF-8

    import sys
    reload(sys)

    # vn.trader模块
    from vnpy.event import EventEngine
    from vnpy.trader.vtEngine import MainEngine
    from vnpy.trader.uiQt import createQApp
    from vnpy.trader.uiMainWindow import MainWindow

    # 加载底层接口
    from vnpy.trader.gateway import ctpGateway, ibGateway

    # 加载上层应用
    from vnpy.trader.app import (riskManager, ctaStrategy, 
                                 spreadTrading, algoTrading)


    #----------------------------------------------------------------------
    def main():
        """主程序入口"""
        # 创建Qt应用对象
        qApp = createQApp()

        # 创建事件引擎
        ee = EventEngine()

        # 创建主引擎
        me = MainEngine(ee)

        # 添加交易接口
        me.addGateway(ctpGateway)
        me.addGateway(ibGateway)

        # 添加上层应用
        me.addApp(riskManager)
        me.addApp(ctaStrategy)
        me.addApp(spreadTrading)
        me.addApp(algoTrading)

        # 创建主窗口
        mw = MainWindow(me, ee)
        mw.showMaximized()

        # 在主线程中启动Qt事件循环
        sys.exit(qApp.exec_())


    if __name__ == '__main__':
        main()

---
### 简介

vn.py是一套基于Python的开源量化交易程序开发框架，起源于国内私募的自主量化交易系统。2015年初项目启动时只是单纯的交易API接口的Python封装。随着业内关注度的上升和社区不断的贡献，目前已经一步步成长为一套全面的交易程序开发框架，用户群体也日渐多样化，包括私募基金、券商自营和资管、期货资管和子公司、高校研究机构和专业个人投资者等。

---
### vn.py原作者
知乎名：用python的交易员

---
### License
MIT
