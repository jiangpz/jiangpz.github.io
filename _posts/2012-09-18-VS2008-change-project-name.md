---
layout: post
title:  "CWnd::OnSize"
excerpt: "CWnd::OnSize."
date:   2012-09-11 22:30:12 +0800
categories: MFC
tags: [MFC]
---
---



在窗口的大小更改后，框架调用该成员函数。


afx_msg void OnSize(
   UINT nType,
   int cx,
   int cy
);

参数

nType

    指定请求的调整大小的类型。 此参数可以是下列值之一：

        SIZE_MAXIMIZED 窗口最大化。

        SIZE_MINIMIZED 窗口最小化。

        SIZE_RESTORED 窗口已调整大小，但是，SIZE_MINIMIZED 和 SIZE_MAXIMIZED 不适用。

        在某些其他窗口最大化时，SIZE_MAXHIDE 发送到所有弹出窗口。

        在某些其他窗口将还原为其以前的大小时，SIZE_MAXSHOW 发送到所有弹出窗口。

cx

    指定工作区的新的宽度。
cy

    指定工作区的新的高度。

备注

如果 SetScrollPos 或 MoveWindow 成员函数用于从 OnSize的子窗口调用，SetScrollPos 或 MoveWindow 的 bRedraw 参数应为非零导致 CWnd 会重新绘制。
说明说明

此成员函数由框架调用提供您的应用程序处理Windows消息。 当接收消息，参数传递给函数以反映结构接收的参数。 如果调用此函数的基类实现，该实现将使用参数最初用消息您提供给函数而非参数。
示例



// Resize the edit control contained in the view to
// fill the entire view when the view's window is
// resized. CMdiView is a CView derived class.
void CMdiView::OnSize(UINT nType, int cx, int cy)
{
   CView::OnSize(nType, cx, cy);
   // Resize edit to fill the whole view.
   // OnSize can be called before OnInitialUpdate
   // so make sure the edit control has been created.
   if (::IsWindow(m_Edit.GetSafeHwnd()))
   {
      m_Edit.MoveWindow (0, 0, cx, cy);
   }
}


要求

Header: afxwin.h
