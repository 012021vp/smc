//This Indicator Contains
//Watermark INDICATOR
//INSIDEBAR INDICATOR
//SMC RULE INDICATOR

//@version=5
indicator(title='SMC tools indicator', overlay=true)

////////Start Watermark indicator////////
//text inputs
title = input.string('Watermark Title', 'Title', group='Watermark settings')
subtitle = input.string('Watermark|subtitle|and|more', 'Subtitle', group='Watermark settings')
//symbol info
symInfoCheck = input.bool(title='Show Symbol Info', defval=true, group='watermark position')
symInfo = syminfo.ticker + ' | ' + timeframe.period + (timeframe.isminutes ? 'M' : na)
date = str.tostring(dayofmonth(time_close)) + '/' + str.tostring(month(time_close)) + '/' + str.tostring(year(time_close))
//text positioning
textVPosition = input.string('top', 'Vertical Position', options=['top', 'middle', 'bottom'], group='watermark position')
textHPosition = input.string('center', 'Horizontal Position', options=['left', 'center', 'right'], group='watermark position')
//symbol info positioning
symVPosition = input.string('bottom', 'Vertical Position', options=['top', 'middle', 'bottom'], group='symbol position')
symHPosition = input.string('center', 'Horizontal Position', options=['left', 'center', 'right'], group='symbol position')
//cell size
width = input.int(0, 'Width', minval=0, maxval=100, tooltip='The width of the cell as a % of the indicator\'s visual space. Optional. By default, auto-adjusts the width based on the text inside the cell. Value 0 has the same effect.', group='cell size')
height = input.int(0, 'Height', minval=0, maxval=100, tooltip='The height of the cell as a % of the indicator\'s visual space. Optional. By default, auto-adjusts the height based on the text inside of the cell. Value 0 has the same effect.', group='cell size')
//title settings
c_title = input.color(color.new(color.black, 0), 'Title Color', group='title settings')
s_title = input.string('large', 'Title Size', options=['tiny', 'small', 'normal', 'large', 'huge', 'auto'], group='title settings')
a_title = input.string('center', 'Title Alignment', options=['center', 'left', 'right'], group='title settings')
//subtitle settings
c_subtitle = input.color(color.new(color.black, 30), 'Subitle Color', group='subtitle settings')
s_subtitle = input.string('normal', 'Subtitle Size', options=['tiny', 'small', 'normal', 'large', 'huge', 'auto'], group='subtitle settings')
a_subtitle = input.string('center', 'Subtitle Alignment', options=['center', 'left', 'right'], group='subtitle settings')

//symbol settings
c_symInfo = input.color(color.new(color.black, 30), 'Subitle Color', group='symbol settings')
s_symInfo = input.string('normal', 'Subtitle Size', options=['tiny', 'small', 'normal', 'large', 'huge', 'auto'], group='symbol settings')
a_symInfo = input.string('center', 'Subtitle Alignment', options=['center', 'left', 'right'], group='symbol settings')
c_bg = input.color(color.new(color.blue, 100), 'Background', group='background')


//text watermark creation
textWatermark = table.new(textVPosition + '_' + textHPosition, 1, 3)
table.cell(textWatermark, 0, 0, title, width, height, c_title, a_title, text_size=s_title, bgcolor=c_bg)
table.cell(textWatermark, 0, 1, subtitle, width, height, c_subtitle, a_subtitle, text_size=s_subtitle, bgcolor=c_bg)
//symbol info watermark creation
symWatermark = table.new(symVPosition + '_' + symHPosition, 5, 5)
if symInfoCheck == true
    table.cell(symWatermark, 0, 1, symInfo, width, height, c_symInfo, a_symInfo, text_size=s_symInfo, bgcolor=c_bg)
    table.cell(symWatermark, 0, 0, date, width, height, c_symInfo, a_symInfo, text_size=s_symInfo, bgcolor=c_bg)
    ////////End Watermark indicator////////
    
    ////////Start Insidebar indicator////////

Inside(position) => high <= high[position] and low >= low[position]

secLast = 1
barcolor(Inside(secLast)? #FF9800: na)

    ////////End Insidebar indicator////////


////////Start Notes indicator////////


table_top_left = 'top_left'
table_top_center = 'top_center'
table_top_right = 'top_right'
table_middle_left = 'middle_left'
table_middle_center = 'middle_center'
table_middle_right = 'middle_right'
table_bottom_left = 'bottom_left'
table_bottom_center = 'bottom_center'
table_bottom_right = 'bottom_right'


i_bgcolor = input.color(color.white, title='Background', group='Notes settings')
i_border_color = input.color(color.white, title='Border', group='Notes settings', inline='border')
i_border_width = input.int(1, title='', minval=0, maxval=3, group='Notes settings', inline='border')
i_table_position = input.string(table_bottom_right, title='Position', options=[table_top_left, table_top_center, table_top_right, table_middle_left, table_middle_center, table_middle_right, table_bottom_left, table_bottom_center, table_bottom_right], group='Notes settings')


table tbl = table.new(i_table_position, columns=1, rows=15, bgcolor=i_bgcolor, frame_color=i_border_color, frame_width=-1, border_color=i_border_color, border_width=i_border_width)

i_show_1 = input.bool(true, title='Note 1', group='Line 1', inline='text1')
i_color_1 = input.color(color.black, title='', group='Line 1', inline='text1')
i_bg_1 = input.color(color.white, title='', group='Line 1', inline='text1')
i_text_1 = input.string('Here you can', title='', group='Line 1', inline='text1')
i_height_1 = input.float(2.5, title='', group='Line 1', inline='text1_2')
i_size_1 = input.string('auto', title='', options=['tiny', 'small', 'normal', 'large', 'auto'], group='Line 1', inline='text1_2')
i_align_1 = input.string('left', title='', options=['center', 'left', 'right'], group='Line 1', inline='text1_2')

if i_show_1
    table.cell(tbl, 0, 0, i_text_1, text_size=i_size_1, text_color=i_color_1, height=i_height_1, bgcolor=i_bg_1, text_halign=i_align_1)


i_show_2 = input.bool(true, title='Note 2', group='Line 2', inline='text2')
i_color_2 = input.color(color.black, title='', group='Line 2', inline='text2')
i_bg_2 = input.color(color.white, title='', group='Line 2', inline='text2')
i_text_2 = input.string('add your notes', title='', group='Line 2', inline='text2')
i_height_2 = input.float(2.5, title='', group='Line 2', inline='text2_2')
i_size_2 = input.string('auto', title='', options=['tiny', 'small', 'normal', 'large', 'auto'], group='Line 2', inline='text2_2')
i_align_2 = input.string('left', title='', options=['center', 'left', 'right'], group='Line 2', inline='text2_2')

if i_show_2
    table.cell(tbl, 0, 1, i_text_2, text_size=i_size_2, text_color=i_color_2, height=i_height_2, bgcolor=i_bg_2, text_halign=i_align_2)

i_show_3 = input.bool(true, title='Note 3', group='Line 3', inline='text3')
i_color_3 = input.color(color.black, title='', group='Line 3', inline='text3')
i_bg_3 = input.color(color.white, title='', group='Line 3', inline='text3')
i_text_3 = input.string('rules', title='', group='Line 3', inline='text3')
i_height_3 = input.float(2.5, title='', group='Line 3', inline='text3_2')
i_size_3 = input.string('auto', title='', options=['tiny', 'small', 'normal', 'large', 'auto'], group='Line 3', inline='text3_2')
i_align_3 = input.string('left', title='', options=['center', 'left', 'right'], group='Line 3', inline='text3_2')

if i_show_3
    table.cell(tbl, 0, 2, i_text_3, text_size=i_size_3, text_color=i_color_3, height=i_height_3, bgcolor=i_bg_3, text_halign=i_align_3)

i_show_4 = input.bool(true, title='Note 4', group='Line 4', inline='text4')
i_color_4 = input.color(color.black, title='', group='Line 4', inline='text4')
i_bg_4 = input.color(color.white, title='', group='Line 4', inline='text4')
i_text_4 = input.string('reminders and so on', title='', group='Line 4', inline='text4')
i_height_4 = input.float(2.5, title='', group='Line 4', inline='text4_2')
i_size_4 = input.string('auto', title='', options=['tiny', 'small', 'normal', 'large', 'auto'], group='Line 4', inline='text4_2')
i_align_4 = input.string('left', title='', options=['center', 'left', 'right'], group='Line 4', inline='text4_2')

if i_show_4
    table.cell(tbl, 0, 3, i_text_4, text_size=i_size_4, text_color=i_color_4, height=i_height_4, bgcolor=i_bg_4, text_halign=i_align_4)


i_show_5 = input.bool(true, title='Note 5', group='Line 5', inline='text5')
i_color_5 = input.color(color.black, title='', group='Line 5', inline='text5')
i_bg_5 = input.color(color.white, title='', group='Line 5', inline='text5')
i_text_5 = input.string('add boxes', title='', group='Line 5', inline='text5')
i_height_5 = input.float(2.5, title='', group='Line 5', inline='text5_2')
i_size_5 = input.string('auto', title='', options=['tiny', 'small', 'normal', 'large', 'auto'], group='Line 5', inline='text5_2')
i_align_5 = input.string('left', title='', options=['center', 'left', 'right'], group='Line 5', inline='text5_2')

if i_show_5
    table.cell(tbl, 0, 4, i_text_5, text_size=i_size_5, text_color=i_color_5, height=i_height_5, bgcolor=i_bg_5, text_halign=i_align_5)


i_show_6 = input.bool(true, title='Note 6', group='Line 6', inline='text6')
i_color_6 = input.color(color.black, title='', group='Line 6', inline='text6')
i_bg_6 = input.color(color.white, title='', group='Line 6', inline='text6')
i_text_6 = input.string('backgrounds', title='', group='Line 6', inline='text6')
i_height_6 = input.float(2.5, title='', group='Line 6', inline='text6_2')
i_size_6 = input.string('auto', title='', options=['tiny', 'small', 'normal', 'large', 'auto'], group='Line 6', inline='text6_2')
i_align_6 = input.string('left', title='', options=['center', 'left', 'right'], group='Line 6', inline='text6_2')

if i_show_6
    table.cell(tbl, 0, 5, i_text_6, text_size=i_size_6, text_color=i_color_6, height=i_height_6, bgcolor=i_bg_6, text_halign=i_align_6)


i_show_7 = input.bool(true, title='Note 7', group='Line 7', inline='text7')
i_color_7 = input.color(color.black, title='', group='Line 7', inline='text7')
i_bg_7 = input.color(color.white, title='', group='Line 7', inline='text7')
i_text_7 = input.string('align center,left or right', title='', group='Line 7', inline='text7')
i_height_7 = input.float(2.5, title='', group='Line 7', inline='text7_2')
i_size_7 = input.string('auto', title='', options=['tiny', 'small', 'normal', 'large', 'auto'], group='Line 7', inline='text7_2')
i_align_7 = input.string('left', title='', options=['center', 'left', 'right'], group='Line 7', inline='text7_2')

if i_show_7
    table.cell(tbl, 0, 6, i_text_7, text_size=i_size_7, text_color=i_color_7, height=i_height_7, bgcolor=i_bg_7, text_halign=i_align_7)


i_show_8 = input.bool(true, title='Note 8', group='Line 8', inline='text8')
i_color_8 = input.color(color.black, title='', group='Line 8', inline='text8')
i_bg_8 = input.color(color.white, title='', group='Line 8', inline='text8')
i_text_8 = input.string('15 rows total', title='', group='Line 8', inline='text8')
i_height_8 = input.float(2.5, title='', group='Line 8', inline='text8_2')
i_size_8 = input.string('auto', title='', options=['tiny', 'small', 'normal', 'large', 'auto'], group='Line 8', inline='text8_2')
i_align_8 = input.string('left', title='', options=['center', 'left', 'right'], group='Line 8', inline='text8_2')

if i_show_8
    table.cell(tbl, 0, 7, i_text_8, text_size=i_size_8, text_color=i_color_8, height=i_height_8, bgcolor=i_bg_8, text_halign=i_align_8)


i_show_9 = input.bool(false, title='Note 9', group='Line 9', inline='text9')
i_color_9 = input.color(color.black, title='', group='Line 9', inline='text9')
i_bg_9 = input.color(color.white, title='', group='Line 9', inline='text9')
i_text_9 = input.string('Note 9', title='', group='Line 9', inline='text9')
i_height_9 = input.float(2.5, title='', group='Line 9', inline='text9_2')
i_size_9 = input.string('auto', title='', options=['tiny', 'small', 'normal', 'large', 'auto'], group='Line 9', inline='text9_2')
i_align_9 = input.string('center', title='', options=['center', 'left', 'right'], group='Line 9', inline='text9_2')

if i_show_9
    table.cell(tbl, 0, 8, i_text_9, text_size=i_size_9, text_color=i_color_9, height=i_height_9, bgcolor=i_bg_9, text_halign=i_align_9)

i_show_10 = input.bool(false, title='Note 10', group='Line 10', inline='text10')
i_color_10 = input.color(color.black, title='', group='Line 10', inline='text10')
i_bg_10 = input.color(color.white, title='', group='Line 10', inline='text10')
i_text_10 = input.string('Note 10', title='', group='Line 10', inline='text10')
i_height_10 = input.float(2.5, title='', group='Line 10', inline='text10_2')
i_size_10 = input.string('auto', title='', options=['tiny', 'small', 'normal', 'large', 'auto'], group='Line 10', inline='text10_2')
i_align_10 = input.string('center', title='', options=['center', 'left', 'right'], group='Line 10', inline='text10_2')

if i_show_10
    table.cell(tbl, 0, 9, i_text_10, text_size=i_size_10, text_color=i_color_10, height=i_height_10, bgcolor=i_bg_10, text_halign=i_align_10)


i_show_11 = input.bool(false, title='Note 11', group='Line 11', inline='text11')
i_color_11 = input.color(color.black, title='', group='Line 11', inline='text11')
i_bg_11 = input.color(color.white, title='', group='Line 11', inline='text11')
i_text_11 = input.string('Note 11', title='', group='Line 11', inline='text11')
i_height_11 = input.float(2.5, title='', group='Line 11', inline='text11_2')
i_size_11 = input.string('auto', title='', options=['tiny', 'small', 'normal', 'large', 'auto'], group='Line 11', inline='text11_2')
i_align_11 = input.string('center', title='', options=['center', 'left', 'right'], group='Line 11', inline='text11_2')

if i_show_11
    table.cell(tbl, 0, 10, i_text_11, text_size=i_size_11, text_color=i_color_11, height=i_height_11, bgcolor=i_bg_11, text_halign=i_align_11)

i_show_12 = input.bool(false, title='Note 12', group='Line 12', inline='text12')
i_color_12 = input.color(color.black, title='', group='Line 12', inline='text12')
i_bg_12 = input.color(color.white, title='', group='Line 12', inline='text12')
i_text_12 = input.string('Note 12', title='', group='Line 12', inline='text12')
i_height_12 = input.float(2.5, title='', group='Line 12', inline='text12_2')
i_size_12 = input.string('auto', title='', options=['tiny', 'small', 'normal', 'large', 'auto'], group='Line 12', inline='text12_2')
i_align_12 = input.string('center', title='', options=['center', 'left', 'right'], group='Line 12', inline='text12_2')

if i_show_12
    table.cell(tbl, 0, 11, i_text_12, text_size=i_size_12, text_color=i_color_12, height=i_height_12, bgcolor=i_bg_12, text_halign=i_align_12)

i_show_13 = input.bool(false, title='Note 13', group='Line 13', inline='text13')
i_color_13 = input.color(color.black, title='', group='Line 13', inline='text13')
i_bg_13 = input.color(color.white, title='', group='Line 13', inline='text13')
i_text_13 = input.string('Note 13', title='', group='Line 13', inline='text13')
i_height_13 = input.float(2.5, title='', group='Line 13', inline='text13_2')
i_size_13 = input.string('auto', title='', options=['tiny', 'small', 'normal', 'large', 'auto'], group='Line 13', inline='text13_2')
i_align_13 = input.string('center', title='', options=['center', 'left', 'right'], group='Line 13', inline='text13_2')

if i_show_13
    table.cell(tbl, 0, 12, i_text_13, text_size=i_size_13, text_color=i_color_13, height=i_height_13, bgcolor=i_bg_13, text_halign=i_align_13)

i_show_14 = input.bool(false, title='Note 14', group='Line 14', inline='text14')
i_color_14 = input.color(color.black, title='', group='Line 14', inline='text14')
i_bg_14 = input.color(color.white, title='', group='Line 14', inline='text14')
i_text_14 = input.string('Note 14', title='', group='Line 14', inline='text14')
i_height_14 = input.float(2.5, title='', group='Line 14', inline='text14_2')
i_size_14 = input.string('auto', title='', options=['tiny', 'small', 'normal', 'large', 'auto'], group='Line 14', inline='text14_2')
i_align_14 = input.string('center', title='', options=['center', 'left', 'right'], group='Line 14', inline='text14_2')

if i_show_14
    table.cell(tbl, 0, 13, i_text_14, text_size=i_size_14, text_color=i_color_14, height=i_height_14, bgcolor=i_bg_14, text_halign=i_align_14)


i_show_15 = input.bool(false, title='Note 15', group='Line 15', inline='text15')
i_color_15 = input.color(color.black, title='', group='Line 15', inline='text15')
i_bg_15 = input.color(color.white, title='', group='Line 15', inline='text15')
i_text_15 = input.string('Note 15', title='', group='Line 15', inline='text15')
i_height_15 = input.float(2.5, title='', group='Line 15', inline='text15_2')
i_size_15 = input.string('auto', title='', options=['tiny', 'small', 'normal', 'large', 'auto'], group='Line 15', inline='text15_2')
i_align_15 = input.string('center', title='', options=['center', 'left', 'right'], group='Line 15', inline='text15_2')

if i_show_15
    table.cell(tbl, 0, 14, i_text_15, text_size=i_size_15, text_color=i_color_15, height=i_height_15, bgcolor=i_bg_15, text_halign=i_align_15)
////////End Notes indicator////////


////////Start no GAPSindicator////////

myOpen = close[1]
myClose = close
myHigh = high
myLow = low

candleColor = myOpen <= myClose ? color.teal : color.red

plotcandle(myOpen, myHigh, myLow, myClose, color=candleColor, bordercolor=candleColor, wickcolor=candleColor)

////////End no GAPSindicator////////
