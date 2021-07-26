---
description: V-DevSuite对默认通用类规则、函数、控件插件进行源码公开
---

# 源码公开

## 开源协议

基于LGPL（GNU Lesser General Public License）

## 源码地址

[前端规则](https://github.com/opensource-vplatform/vplatform-plugin-rule-client)

[前端函数](https://github.com/opensource-vplatform/vplatform-plugin-function-client)

[前端控件](https://github.com/opensource-vplatform/vplatform-plugin-widget-smartclient)

[后端规则](https://github.com/opensource-vplatform/vplatform-plugin-rule-server)

[后端函数](https://github.com/opensource-vplatform/vplatform-plugin-function-server)

_注：release branch为正式版，main branch为开发版_

## 开源进度_（更新时间2021-07-26）_

### 1. 已开源的插件

{% tabs %}
{% tab title="后端规则" %}
SetEntityVarControlValue--给界面实体/控件/变量赋值, AbortRule--中断规则, AddTableRecord--新增实体记录, SetLoopVariant--给循环变量赋值, ExecExpression--执行函数表达式, ClearEntityData--清除实体记录, ExceptionAbort--异常中断, AbortLoop--中断循环 , DeleteConditionRelationData-删除数据库中的记录, EntityConditionRemove-删除实体记录, EntityRecordRecycling-实体记录循环处理, GenerateXMLOrJSON-配置数据生成, UpdateRecord-保存实体到数据
{% endtab %}

{% tab title="后端函数" %}
ABS, Acos, AddThousandBits, AsciiToUnicode, Asin, Atan, AvgColumnFunc, Ceiling, ChangeMoneyToChinese, CheckCertCodeFun, CheckChinese, ChineseToUnicode, Compare, ConcatStr, Contains, ConvertFunc, ConvertPageNumber, ConvertVarToEntityColumn, CopyFileByFileId, Cos, Cosh, DateAddFunc, DateConvert, Datediff, DateSub, DateTimeNow, DateTimeToUnixtimestamp, DateToString, DecodeBASE64, DecodeURIComponent, DecryptFunc, Divrem, DowdloadFileToFileSystem, DownloadFromFtp, E, EncodeBASE64, EncodeURIComponent, EncryptFunc, EncryptionFunc, EndsWith, EvalExpression, Exp, Floor, Format, GenerateUUID, GetAgeByIdCard, GetAllParentIds, GetConditionColumnValue, GetDateSection, GetDistance, GetEntityRowCountFunc, GetFileInfo, GetFileUrlByFileId, GetFirstRowColumnValue, GetImageUrl, GetIPAddressFunc, GetLength, Log10, Max, LogFunc, Min, Pai, Pow, Sin, Sinh, Tan, Tanh, UnixtimestampToDateTime, ServerDive, Trim, TrimEnd, TrimStart, IsWhiteOrSpace, Insert, GetIPAddressFunc, UnicodeToChinese, UnicodeToAscii, IsEmpty, GetSystemVariable, DecryptFunc, ServerSubtract, IsNullOrEmptyFunc, ListToStringFunc, PadRight, ServerAdd, Random, RecyclingSequenceNumber, Remainder, Remove, ReplaceByIndex, ReplaceFunc, Round, ServerDivide, ServerMultiply, ServerSubtract, ShortDateNow, ShortTimeNow, Sign, StandardMD5Encrypt, StartsWith, Substring, ToLower, TotalColumnFunc, ToUpper, TreeDataUpwardCollect, Truncate, UploadToFtp, V3If, VConvertEntityToJsonFunc, VConvertEntityToXMLFunc, VRestoreJsonToEntityFunc, VRestoreXMLToEntityFunc, LastIndexOf, Null, MaxColumn, NumberCodeAdd, PadLeft, PadRight, MD5EncryptByUTF8, GetProperty, GenerateSequenceNumber, GenerateSequenceNumberQuick, GetDataBaseType, GetLngOrLatByAddr, GetLoactionPlace, GetSerialNumberFunc, GetTableData, GetZoomLevel, HasRecordFunc, IndexOf, IsNull, MD5Encrypt, MinColumn, Sqrt
{% endtab %}

{% tab title="前端规则" %}
AbortLoop--中断循环, AbortRule--中断规则, AddTableRecord-新增实体记录, Webrule\_ShowMessageWhenChanged--判断指定实体的数据是否发生变化, Webrule\_ShowMessage--显示设设置提示信息, Webrule\_SetLoopVariant--给循环变量赋值, Webrule\_SetControlPropertys--控件属性设置, Webrule\_SelectionConfirm--退出窗体, Webrule\_ResetSelectedControlValue--清空控件数值, Webrule\_RefreshSystemVariable--刷新构建变量的值, Webrule\_Progress--进度条显示隐藏, Webrule\_MakeControlRVE--控制控件的只读、使能、显示, Webrule\_LocateSelectRecord--记录选中/取消选中, LocateCurrentRecord--记录定位, PageVisibleControl--页签显示控制, TreeNodeMoveUpDownEditor--实体树形操作
{% endtab %}

{% tab title="前端函数" %}
Acos ,Add ,AsciiToUnicode ,Asin ,Atan ,BigMul ,Ceiling ,ChineseToUnicode ,Compare ,ConcatStr ,Contains ,ConvertAbsoluteValue ,Cos ,Cosh ,DateAdd ,DateConvert ,DateSub ,DateTimeNow ,DateTimeToUnixtimestamp ,DateToString ,Datediff ,Divide ,Divrem ,E ,EndsWith ,Exp ,Floor ,Format ,GetDateSection ,GetLength ,IndexOf ,Insert ,LastIndexOf ,LocateDateTimeNow ,Log ,Log10 ,Max ,Min ,Multiply ,PadLeft ,PadRight ,Pai ,Pow ,Random ,Remainder ,Remove ,Replace ,ReplaceByIndex ,Round ,ShortDateNow ,ShortTimeNow ,Sign ,Sin ,Sinh ,Sqrt ,StartsWith ,Substring ,Subtract ,Tan ,Tanh ,ToLower ,ToUpper ,Trim ,TrimEnd ,TrimStart ,Truncate ,UnicodeToAscii ,UnicodeToChinese ,UnixtimestampToDateTime ,GetAgeByIdCard ,AvgColumn ,ChangeMoneyToChinese ,CheckChinese ,Convert ,ConvertUnit ,ConvertVarToEntityColumn ,DateTimeToChinese ,DecodeURIComponent ,EncodeURIComponent ,EntityToVar ,EvalExpression ,GetAgeByIdCard ,GetBirthdayByIdCard ,GetBrowserInfo ,GetCurrentRecordIndex ,GetEntityCurrentColumnValue ,GetEntityRowCount ,GetEntitySelectedRowCount ,GetFirstRowColumnValue ,GetLocalStorage ,GetRowNum ,GetSystemCurrentTimeMillis ,IsNull ,IsNullOrEmpty ,ListToString ,MaxColumn ,MinColumn ,NumiceToChinese ,PrintToBrowserConsole ,SetLocalStorage ,SetRowNum ,TotalColumn ,V3If ,VarToEntity
{% endtab %}

{% tab title="前端控件" %}
JGButton ,JGImage ,JGTimer ,JGHyperLink
{% endtab %}
{% endtabs %}

### 2. 测试验证中的插件

{% tabs %}
{% tab title="后端规则" %}
CallWebApi-调用webapi, CallWebService-调用webservice, ServerRestoreXMLOrJSON-配置数据还原, DataBaseDataToInterfaceEntity-从数据库获取数据到实体, ModifyDataBaseRecord-修改数据库中的记录, ExecuteVoidQuery-执行无返回值的查询, ImportProjectToDBOrEntity-Project导入到数据库表或实体, DataBaseDataToInterfaceEntity-从数据库获取数据到实体, CopyRecordBetweenEntity-实体间复制记录, ServPrintDataTrans-报表打印数据转换, CopyRecordBetweenTables-表间数据复制
{% endtab %}

{% tab title="后端函数" %}
已改造完毕
{% endtab %}

{% tab title="前端规则" %}
RefreshControlItems--刷新控件的候选项, PrintOperation--打印及预览操作, TreeGridStatistics-树表数值字段向上汇总, TreeDisplayOper--树节点展开折叠, UpdateRecord--保存实体到数据库, Webrule\_CalculateToColumn--计算公式的值并赋值给指定字段, Webrule\_ClearInterfaceEntityData--清除界面实体中的记录, Webrule\_CopyTreeDataBetweenEntities--树形结构实体间数据复制, Webrule\_CursorJumpControl--光标跳转控制, Webrule\_DeleteListSelectRow--删除实体记录, SetEntityVarControlValue--给界面实体/控件/变量赋值, AddDataBaseRecord--新增数据库记录, InterfaceEntityRecordRecycling---界面实体记录循环处理, MakeCertPic--生成数据验证码, ModifyDataBaseRecord--修改数据库中的记录, RecordReferenceCheck--记录引用检查, RestoreXMLOrJSON--配置数据还原, VucRedirector--统一认证跳转, GetRecordCount--获取数据库表中的记录, I18nOperation--多语言操作, ImportExcelToDB--Excel导入到数据库表, JGStepsOperation 步骤条操作
{% endtab %}

{% tab title="前端函数" %}
暂无...
{% endtab %}

{% tab title="前端控件" %}
JGCheckBox, JGFloatBox, JGLongTextBox, JGPassword, JGTextBox, JGBaseDictBox, JGComboBox, JGDateTimePicker, JGIntegerBox, JGCheckBoxGroup, JGRadioGroup, JGLongDateTimePicker, JGPeriod, JGPercent
{% endtab %}
{% endtabs %}

### 3. 准备开源的插件

{% tabs %}
{% tab title="后端规则" %}
ExecuteRuleSet, DataBaseDataToInterfaceEntity, CopyRecordBetweenEntity, ModifyDataBaseRecord, ImportExcelToDBOrEntity, ExportDBOrEntityDataToExcel, ServPrintDataTrans, CopyRecordBetweenTables
{% endtab %}

{% tab title="后端函数" %}
已改造完毕
{% endtab %}

{% tab title="前端规则" %}
ExecuteRuleSet ,OpenComponentReturnData ,OpenLink ,PrdOpenBizFrameReturnData ,Attachmentoperation ,CallWebApi ,CancelCloseWindow ,CheckAppVersion ,CheckCertCode ,CheckRequired ,CheckTableFieldValuesUnique ,CheckUnique ,CompareEntityAndTableData ,CompareEntityData ,CopyDataBetweenTables ,CopyEntityRecord ,CopyTreeDataBetweenTables ,DataBaseDataToInterfaceEntity ,DataBaseDataToReport ,DataValidationEditor ,DeleteConditionRelationData ,DocumentsConverted ,DynamicCrossDataToInterfaceEntity ,EntityColumnTurnRow ,ExecExpression ,ExecuteNativeMethod ,ExportData ,ExportDataToExcel ,ExportTableData ,GenerateBillCode ,GenerateXMLOrJSON ,GetClosestPosition
{% endtab %}

{% tab title="前端函数" %}
Webfunc\_ArgsToArray, Webfunc\_Decrypt, Webfunc\_DecryptFunc, Webfunc\_DeleteCookie, Webfunc\_DeleteFileByFileId, Webfunc\_Encrypt, Webfunc\_EncryptFunc, Webfunc\_FindControl, Webfunc\_GenerateSequenceNumber, Webfunc\_GenerateSequenceNumberQuick, Webfunc\_GenerateTextByTemplate, , Webfunc\_GenerateUUID, Webfunc\_GetChartClickData, Webfunc\_GetComponentCode, Webfunc\_GetContextPath, Webfunc\_GetControlProperty, , Webfunc\_GetCookie, Webfunc\_GetCurrentCalendarMonth, Webfunc\_GetCurrentWindowInstanceCode, Webfunc\_GetDataBaseType, Webfunc\_GetDynamicColumnIdentity, GetFileInfo, GetGridComp, GetHost, GetImageUrlByFileId, GetIPAddress, GetloginUserNum, GetRequestParmByKey, GetSelectedDateToEntity, GetSerialNumber, GetTableData, GetTreeEntityIds, GetWidgetSize, GetWindowCode, HasRecord, IsExistWindowInstanceCode, IsLeaf, IsLogin, IsSelectedRecord, MD5Encrypt, MD5EncryptByUTF8, Null, NumberCodeAdd, RecyclingSequenceNumber, ScrollToPosition, SelectedDateFromEntity, SelectOrQuitAllRecords, SetControlProperty, , SetCookie, SetCurrentWindowTitle, SetGridColReadOnly, SetGridColTitle, SetGridColVisble, SetRecordValue, SetToolBarText, SetWindowState, StandardMD5Encrypt, TreeNodePath, VConvertEntityToJson, VConvertEntityToXML, VConvertKeyValueEntityToJson, VRestoreJsonToEntity, VRestoreXMLToEntity
{% endtab %}

{% tab title="前端控件" %}
JGTabControl, JGComponentContainer, JGQueryConditionPanel, JGButtonGroup, JGDiv, JGNavigator, JGStartMenu, JGRichTextEditor, JGRichTextViewer, JGAttachment, JGDataGrid, JGTreeGrid, JGTreeView, JGChart, JGReport, JGRecordPaging, JGActivityPanel, JGWorkFlowGraph, JGPropertyEditor, JGCalendar, JGSteps, JGPortal, JGWebBrowser, JGFormLayout, JGGroupPanel, JGImageCutter
{% endtab %}
{% endtabs %}

