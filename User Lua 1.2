-- encoding: UTF-8

_CHINESE_DIGITS = {
  [0] = "〇",
  [1] = "一",
  [2] = "二",
  [3] = "三",
  [4] = "四",
  [5] = "五",
  [6] = "六",
  [7] = "七",
  [8] = "八",
  [9] = "九",
  [10] = "十",
}
_DATE_PATTERN = "^(%d+)-(%d+)-(%d+)$"
_TIME_PATTERN = "^(%d+):(%d+)$"

function GetChineseMathNum(num)
  local ret
  if num < 10 then
    ret = _CHINESE_DIGITS[num]
  elseif num < 20 then
    ret = _CHINESE_DIGITS[10]
    if num > 10 then
      ret = ret .. _CHINESE_DIGITS[num % 10]
    end
  elseif num < 100 then
    local mod = num % 10
    ret = _CHINESE_DIGITS[(num - mod) / 10] .. _CHINESE_DIGITS[10]
    if mod > 0 then
      ret = ret .. _CHINESE_DIGITS[mod]
    end
  else
    error("Invalid number")
  end
  return ret
end

function GetChineseNonMathNum(num)
  local ret = ""
  for ch in tostring(num):gmatch(".") do
    if ch >= "0" and ch <= "9" then
      ch = _CHINESE_DIGITS[tonumber(ch)]
    end
    ret = ret .. ch
  end
  return ret
end

function _VerifyTime(hour, minute)
  if hour < 0 or hour > 23 or minute < 0 or minute > 59 then
    error("Invalid time")
  end
end

function _VerifyDate(month, day)
  if month < 1 or month > 12 or day < 1 or day > _MONTH_TABLE_LEAF[month] then
    error("Invalid date")
  end
end

function _VerifyDateWithYear(year, month, day)
  _VerifyDate(month, day)
  if year < 1 or year > 9999 then
    error("Invalid year")
  end
  if month == 2 and day == 29 then
    if year % 400 ~= 0 and year % 100 == 0 then
      error("Invalid lunar day")
    end
    if year % 4 ~= 0 then
      error("Invalid lunar day")
    end
  end
end

function GetChineseDate(y, m, d, full)
  if full then
    return GetChineseNonMathNum(y) .. "年" ..
           GetChineseMathNum(m) .. "月" ..
           GetChineseMathNum(d) .. "日"
  else
    return y .. "年" .. m .. "月" .. d .. "日"
  end
end

function GetChineseTime(h, m, full)
  if full then
    local ret = GetChineseMathNum(h) .. "时"
    if m > 0 then
      ret = ret .. GetChineseMathNum(m) .. "分"
    end
    return ret
  else
    return h .. "时" .. m .. "分"
  end
end

function NormalizeDate(y, m, d)
  return string.format("%d-%02d-%02d", y, m, d)
end

function NormalizeTime(h, m)
  return string.format("%02d:%02d", h, m)
end

function GetTime(input)
  local now = input
  if #input == 0 then
    now = os.date("%H:%M")
  end
  local hour, minute
  now:gsub(_TIME_PATTERN, function(h, m)
    hour = tonumber(h)
    minute = tonumber(m)
  end)
  _VerifyTime(hour, minute)
  return {
    NormalizeTime(hour, minute),
    GetChineseTime(hour, minute, false),
    GetChineseTime(hour, minute, true),
  }
end

function GetDate(input)
  local now = input
  if #input == 0 then
    now = os.date("%Y-%m-%d")
  end
  local year, month, day
  now:gsub(_DATE_PATTERN, function(y, m, d)
    year = tonumber(y)
    month = tonumber(m)
    day = tonumber(d)
  end)
  _VerifyDateWithYear(year, month, day)
  return {
    GetChineseDate(year, month, day, false),
    NormalizeDate(year, month, day),
    GetChineseDate(year, month, day, true),
  }
end

_MATH_KEYWORDS = {
  "abs", "acos", "asin", "atan", "atan2", "ceil", "cos", "cosh", "deg", "exp",
  "floor", "fmod", "frexp", "ldexp", "log", "log10", "max", "min", "modf", "pi",
  "pow", "rad", "random", "randomseed", "sin", "sinh", "sqrt", "tan", "tanh",
}

function _AddMathKeyword(input)
  local ret = input
  for _, keyword in pairs(_MATH_KEYWORDS) do
    ret = ret:gsub(string.format("([^%%a\.])(%s\(.-\))", keyword), "%1math\.%2")
    ret = ret:gsub(string.format("^(%s\(.-\))", keyword), "math\.%1")
  end
  return ret
end

function Compute(input)
  local expr = "return " .. _AddMathKeyword(input)
  local func = loadstring(expr)
  if func == nil then
    return "-- 未完整表达式 --"
  end
  local ret = func()
  if ret == math.huge then -- div/0
    return "-- 计算错误 --"
  end
  if ret ~= ret then
    -- We rely on the property that NaN is the only value not equal to itself.
    return "-- 计算错误 --"
  end
  return ret
end

math.randomseed(os.time())

_MONTH_TABLE_NORMAL = { 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 }
_MONTH_TABLE_LEAF = { 31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 }

function _CompareMonthAndDay(month1, day1, month2, day2)
  if month1 < month2 then
    return -1
  elseif month1 > month2 then
    return 1
  elseif day1 < day2 then
    return -1
  elseif day1 > day2 then
    return 1
  else
    return 0
  end
end

function GetCurrentTime()
  return GetTime("")
end

function GetDay()
  return GetDate("")
end

ime.register_command("sj", "GetTime", "输入时间", "alpha", "输入可选时间，例如12:34")
ime.register_command("rq", "GetDate", "输入日期", "alpha", "输入可选日期，例如2008-08-08")
ime.register_command("js", "Compute", "计算模式", "none", "输入表达式，例如3*log(4+2)")
ime.register_trigger("GetCurrentTime", "显示时间", {}, {'时间'})
ime.register_trigger("GetDay", "显示日期", {}, {'日期'})

---------------------------------------------------------------------------------------------------

function GetYesterday_2()
  local today
	today = os.date("%Y%m%d")
	count = 3
	local year, month, day
	year = tonumber(string.sub(today, 1, 4))
	month = tonumber(string.sub(today, 5, 6))
	day = tonumber(string.sub(today, 7, 8))
	local count
	for count = 1, 3 do
		if day == 1 then
			if month == 3 then
				month = 2
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					day = 28
				end
			elseif month ~= 1 then
				month = month - 1
				day = _MONTH_TABLE_NORMAL[month]
			else
				month = 12
				day = 31
			end
		else
			day = day - 1
		end
	end
	return month .. "月" .. day .. "日"
end

function GetYesterday_1()
	local today
	today = os.date("%Y%m%d")
	local year, month, day
	year = tonumber(string.sub(today, 1, 4))
	month = tonumber(string.sub(today, 5, 6))
	day = tonumber(string.sub(today, 7, 8))
	local count
	for count = 1, 2 do
		if day == 1 then
			if month == 3 then
				month = 2
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					day = 28
				end
			elseif month ~= 1 then
				month = month - 1
				day = _MONTH_TABLE_NORMAL[month]
			else
				month = 12
				day = 31
			end
		else
			day = day - 1
		end
	end
	return month .. "月" .. day .. "日"
end

function GetYesterday()
	local today
	today = os.date("%Y%m%d")
	local year, month, day
	year = tonumber(string.sub(today, 1, 4))
	month = tonumber(string.sub(today, 5, 6))
	day = tonumber(string.sub(today, 7, 8))
	if day == 1 then
		if month == 3 then
			month = 2
			if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
				day = 29
			else
				day = 28
			end
		elseif month ~= 1 then
			month = month - 1
			day = _MONTH_TABLE_NORMAL[month]
		else
			month = 12
			day = 31
		end
	else
		day = day - 1
	end
	return month .. "月" .. day .. "日"
end

function GetToday()
  local month, day
  month = tonumber(os.date("%m"))
  day = tonumber(os.date("%d"))
  return month .. "月" .. day .. "日"
end

function GetTomorrow()
	local today
	today = os.date("%Y%m%d")
	local year, month, day
	year = tonumber(string.sub(today, 1, 4))
	month = tonumber(string.sub(today, 5, 6))
	day = tonumber(string.sub(today, 7, 8))
	if month == 2 and day == 28 then
		if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
			day = 29
		else
			month = month + 1
			day = 1
		end
	elseif day == _MONTH_TABLE_LEAF[month] then
		if month == 12 then
			month = 1
			day = 1
		else
			month = month + 1
			day = 1
		end
	else
		day = day + 1	
	end
	return month .. "月" .. day .. "日"
end

function GetTomorrow_1()
	local today
	today = os.date("%Y%m%d")
	local year, month, day
	year = tonumber(string.sub(today, 1, 4))
	month = tonumber(string.sub(today, 5, 6))
	day = tonumber(string.sub(today, 7, 8))
	local count
	for count = 1, 2 do
		if month == 2 and day == 28 then
			if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
				day = 29
			else
				month = month + 1
				day = 1
			end
		elseif day == _MONTH_TABLE_LEAF[month] then
			if month == 12 then
				month = 1
				day = 1
			else
				month = month + 1
				day = 1
			end
		else
			day = day + 1	
		end
	end
	return month .. "月" .. day .. "日"
end

function GetTomorrow_2()
	local today
	today = os.date("%Y%m%d")
	local year, month, day
	year = tonumber(string.sub(today, 1, 4))
	month = tonumber(string.sub(today, 5, 6))
	day = tonumber(string.sub(today, 7, 8))
	for count = 1, 3 do
		if month == 2 and day == 28 then
			if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
				day = 29
			else
				month = month + 1
				day = 1
			end
		elseif day == _MONTH_TABLE_LEAF[month] then
			if month == 12 then
				month = 1
				day = 1
			else
				month = month + 1
				day = 1
			end
		else
			day = day + 1	
		end
	end
	return month .. "月" .. day .. "日"
end

ime.register_trigger("GetYesterday_2", "显示日期", {}, {'大前天'})
ime.register_trigger("GetYesterday_1", "显示日期", {}, {'前天'})
ime.register_trigger("GetYesterday", "显示日期", {}, {'昨天'})
ime.register_trigger("GetToday", "显示日期", {}, {'今天'})
ime.register_trigger("GetTomorrow", "显示日期", {}, {'明天'})
ime.register_trigger("GetTomorrow_1", "显示日期", {}, {'后天'})
ime.register_trigger("GetTomorrow_2", "显示日期", {}, {'大后天'})

function GetLastMonth_1()
	local month
	month = tonumber(os.date("%m"))
	if month < 3 then
		if month == 1 then
			month = 11
		else
			month = 12
		end
	else
		month = month - 2
	end
	return month .. "月"
end

function GetLastMonth()
	local month
	month = tonumber(os.date("%m"))
	if month ~= 1 then
		month = month - 1
	else
		month = 12
	end
	return month .. "月"
end

function GetThisMonth()
	local month
	month = tonumber(os.date("%m"))
	return month .. "月"
end

function GetNextMonth()
	local month
	month = tonumber(os.date("%m"))
	if month ~= 12 then
		month = month + 1
	else
		month = 1
	end
	return month .. "月"
end

function GetNextMonth_1()
	local month
	month = tonumber(os.date("%m"))
	if month > 10 then
		if month == 11 then
			month = 1
		else
			month = 2
		end
	else
		month = month + 2
	end
	return month .. "月"
end

ime.register_trigger("GetLastMonth_1", "显示日期", {}, {'上上月', '上上个月'})
ime.register_trigger("GetLastMonth", "显示日期", {}, {'上月', '上个月'})
ime.register_trigger("GetThisMonth", "显示日期", {}, {'这月', '本月', '这个月'})
ime.register_trigger("GetNextMonth", "显示日期", {}, {'下月', '下个月'})
ime.register_trigger("GetNextMonth_1", "显示日期", {}, {'下下月', '下下个月'})

function GetLastYear_2()
	local year
	year = tonumber(os.date("%Y"))
	year = year - 3
	return year .. "年"
end

function GetLastYear_1()
	local year
	year = tonumber(os.date("%Y"))
	year = year - 2
	return year .. "年"
end

function GetLastYear()
	local year
	year = tonumber(os.date("%Y"))
	year = year - 1
	return year .. "年"
end

function GetThisYear()
	local year
	year = tonumber(os.date("%Y"))
	return year .. "年"
end

function GetNextYear()
	local year
	year = tonumber(os.date("%Y"))
	year = year + 1
	return year .. "年"
end

function GetNextYear_1()
	local year
	year = tonumber(os.date("%Y"))
	year = year + 2
	return year .. "年"
end

function GetNextYear_2()
	local year
	year = tonumber(os.date("%Y"))
	year = year + 3
	return year .. "年"
end

ime.register_trigger("GetLastYear_2", "显示日期", {}, {'大前年'})
ime.register_trigger("GetLastYear_1", "显示日期", {}, {'前年'})
ime.register_trigger("GetLastYear", "显示日期", {}, {'去年', '上年'})
ime.register_trigger("GetThisYear", "显示日期", {}, {'今年', '本年'})
ime.register_trigger("GetNextYear", "显示日期", {}, {'明年', '下年'})
ime.register_trigger("GetNextYear_1", "显示日期", {}, {'后年'})
ime.register_trigger("GetNextYear_2", "显示日期", {}, {'大后年'})

function GetThisMonday()
	local today
	today = os.date("%Y%m%d")
	local year, month, day
	year = tonumber(string.sub(today, 1, 4))
	month = tonumber(string.sub(today, 5, 6))
	day = tonumber(string.sub(today, 7, 8))
	local nday, count
	nday = os.date("%w")
	count = nday - 1
	if count == 0 then
		return month .. "月" .. day .. "日"
	elseif count > 0 then
		for nday = 1, count do
			if day == 1 then
				if month == 3 then
					month = 2
					if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
						day = 29
					else
						day = 28
					end
				elseif month ~= 1 then
					month = month - 1
					day = _MONTH_TABLE_NORMAL[month]
				else
					month = 12
					day = 31
				end
			else
				day = day - 1
			end
		end
		return month .. "月" .. day .. "日"
	else
		for nday = 1, 6 do
			if day == 1 then
				if month == 3 then
					month = 2
					if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
						day = 29
					else
						day = 28
					end
				elseif month ~= 1 then
					month = month - 1
					day = _MONTH_TABLE_NORMAL[month]
				else
					month = 12
					day = 31
				end
			else
				day = day - 1
			end
		end
		return month .. "月" .. day .. "日"
	end
end

function GetThisTuesday()
	local today
	today = os.date("%Y%m%d")
	local year, month, day
	year = tonumber(string.sub(today, 1, 4))
	month = tonumber(string.sub(today, 5, 6))
	day = tonumber(string.sub(today, 7, 8))
	local nday, count
	nday = os.date("%w")
	count = nday - 2
	if count == 0 then
		return month .. "月" .. day .. "日"
	elseif count > 0 then
		for nday = 1, count do
			if day == 1 then
				if month == 3 then
					month = 2
					if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
						day = 29
					else
						day = 28
					end
				elseif month ~= 1 then
					month = month - 1
					day = _MONTH_TABLE_NORMAL[month]
				else
					month = 12
					day = 31
				end
			else
				day = day - 1
			end
		end
		return month .. "月" .. day .. "日"
	elseif count == -2 then	
		for nday = 1, 5 do
			if day == 1 then
				if month == 3 then
					month = 2
					if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
						day = 29
					else
						day = 28
					end
				elseif month ~= 1 then
					month = month - 1
					day = _MONTH_TABLE_NORMAL[month]
				else
					month = 12
					day = 31
				end
			else
				day = day - 1
			end
		end
		return month .. "月" .. day .. "日"
	else
		if month == 2 and day == 28 then
			if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
				day = 29
			else
				month = month + 1
				day = 1
			end
		elseif day == _MONTH_TABLE_LEAF[month] then
			month = month + 1
			day = 1
		else
			day = day + 1	
		end
			return month .. "月" .. day .. "日"
	end
end

function GetThisWednesday()
	local today
	today = os.date("%Y%m%d")
	local year, month, day
	year = tonumber(string.sub(today, 1, 4))
	month = tonumber(string.sub(today, 5, 6))
	day = tonumber(string.sub(today, 7, 8))
	local nday, count
	nday = os.date("%w")
	count = nday - 3
	if count == 0 then
		return month .. "月" .. day .. "日"
	elseif count > 0 then
		for nday = 1, count do
			if day == 1 then
				if month == 3 then
					month = 2
					if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
						day = 29
					else
						day = 28
					end
				elseif month ~= 1 then
					month = month - 1
					day = _MONTH_TABLE_NORMAL[month]
				else
					month = 12
					day = 31
				end
			else
				day = day - 1
			end
		end
		return month .. "月" .. day .. "日"
	elseif count == -3 then
		for nday = 1, 4 do
			if day == 1 then
				if month == 3 then
					month = 2
					if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
						day = 29
					else
						day = 28
					end
				elseif month ~= 1 then
					month = month - 1
					day = _MONTH_TABLE_NORMAL[month]
				else
					month = 12
					day = 31
				end
			else
				day = day - 1
			end
		end
		return month .. "月" .. day .. "日"
	else
		for nday = count, -1 do
			if month == 2 and day == 28 then
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					month = month + 1
					day = 1
				end
			elseif day == _MONTH_TABLE_LEAF[month] then
				month = month + 1
				day = 1
			else
				day = day + 1	
			end
		end
		return month .. "月" .. day .. "日"
	end
end

function GetThisThursday()
	local today
	today = os.date("%Y%m%d")
	local year, month, day
	year = tonumber(string.sub(today, 1, 4))
	month = tonumber(string.sub(today, 5, 6))
	day = tonumber(string.sub(today, 7, 8))
	local nday, count
	nday = os.date("%w")
	count = nday - 4
	if count == 0 then
		return month .. "月" .. day .. "日"
	elseif count > 0 then
		for nday = 1, count do
			if day == 1 then
				if month == 3 then
					month = 2
					if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
						day = 29
					else
						day = 28
					end
				elseif month ~= 1 then
					month = month - 1
					day = _MONTH_TABLE_NORMAL[month]
				else
					month = 12
					day = 31
				end
			else
				day = day - 1
			end
		end
		return month .. "月" .. day .. "日"
	elseif count == -4 then
		for nday = 1, 3 do
			if day == 1 then
				if month == 3 then
					month = 2
					if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
						day = 29
					else
						day = 28
					end
				elseif month ~= 1 then
					month = month - 1
					day = _MONTH_TABLE_NORMAL[month]
				else
					month = 12
					day = 31
				end
			else
				day = day - 1
			end
		end
		return month .. "月" .. day .. "日"
	else
		for nday = count, -1 do
			if month == 2 and day == 28 then
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					month = month + 1
					day = 1
				end
			elseif day == _MONTH_TABLE_LEAF[month] then
				month = month + 1
				day = 1
			else
				day = day + 1	
			end
		end
		return month .. "月" .. day .. "日"
	end
end

function GetThisFriday()
	local today
	today = os.date("%Y%m%d")
	local year, month, day
	year = tonumber(string.sub(today, 1, 4))
	month = tonumber(string.sub(today, 5, 6))
	day = tonumber(string.sub(today, 7, 8))
	local nday, count
	nday = os.date("%w")
	count = nday - 5
	if count == 0 then
		return month .. "月" .. day .. "日"
	elseif count > 0 then
		for nday = 1, count do
			if day == 1 then
				if month == 3 then
					month = 2
					if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
						day = 29
					else
						day = 28
					end
				elseif month ~= 1 then
					month = month - 1
					day = _MONTH_TABLE_NORMAL[month]
				else
					month = 12
					day = 31
				end
			else
				day = day - 1
			end
		end
		return month .. "月" .. day .. "日"
	elseif count == -5 then
		for nday = 1, 2 do
			if day == 1 then
				if month == 3 then
					month = 2
					if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
						day = 29
					else
						day = 28
					end
				elseif month ~= 1 then
					month = month - 1
					day = _MONTH_TABLE_NORMAL[month]
				else
					month = 12
					day = 31
				end
			else
				day = day - 1
			end
		end
		return month .. "月" .. day .. "日"
	else
		for nday = count, -1 do
			if month == 2 and day == 28 then
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					month = month + 1
					day = 1
				end
			elseif day == _MONTH_TABLE_LEAF[month] then
				month = month + 1
				day = 1
			else
				day = day + 1	
			end
		end
		return month .. "月" .. day .. "日"
	end
end

function GetThisSaturday()
	local today
	today = os.date("%Y%m%d")
	local year, month, day
	year = tonumber(string.sub(today, 1, 4))
	month = tonumber(string.sub(today, 5, 6))
	day = tonumber(string.sub(today, 7, 8))
	local nday, count
	nday = os.date("%w")
	count = nday - 6
	if count == 0 then
		return month .. "月" .. day .. "日"
	elseif count == -6 then
		if day == 1 then
			if month == 3 then
				month = 2
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					day = 28
				end
			elseif month ~= 1 then
				month = month - 1
				day = _MONTH_TABLE_NORMAL[month]
			else
				month = 12
				day = 31
			end
		else
			day = day - 1
		end
	return month .. "月" .. day .. "日"
	else
		for nday = count, -1 do
			if month == 2 and day == 28 then
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					month = month + 1
					day = 1
				end
			elseif day == _MONTH_TABLE_LEAF[month] then
				month = month + 1
				day = 1
			else
				day = day + 1	
			end
		end
		return month .. "月" .. day .. "日"
	end
end

function GetThisSunday()
	local today
	today = os.date("%Y%m%d")
	local year, month, day
	year = tonumber(string.sub(today, 1, 4))
	month = tonumber(string.sub(today, 5, 6))
	day = tonumber(string.sub(today, 7, 8))
	local nday, count
	nday = os.date("%w")
	count = nday - 7
	if count == -7 then
		return month .. "月" .. day .. "日"
	else
		for nday = count, -1 do
			if month == 2 and day == 28 then
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					month = month + 1
					day = 1
				end
			elseif day == _MONTH_TABLE_LEAF[month] then
				month = month + 1
				day = 1
			else
				day = day + 1	
			end
		end
		return month .. "月" .. day .. "日"
	end
end

ime.register_trigger("GetThisMonday", "显示日期", {}, {'周一', '星期一', '礼拜一', '这周一', '这星期一', '这礼拜一', '本周一', '本星期一', '本礼拜一'})
ime.register_trigger("GetThisTuesday", "显示日期", {}, {'周二', '星期二', '礼拜二', '这周二', '这星期二', '这礼拜二', '本周二', '本星期二', '本礼拜二'})
ime.register_trigger("GetThisWednesday", "显示日期", {}, {'周三', '星期三', '礼拜三', '这周三', '这星期三', '这礼拜三', '本周三', '本星期三', '本礼拜三'})
ime.register_trigger("GetThisThursday", "显示日期", {}, {'周四', '星期四', '礼拜四', '这周四', '这星期四', '礼拜四', '本周四', '本星期四', '本礼拜四'})
ime.register_trigger("GetThisFriday", "显示日期", {}, {'周五', '星期五', '礼拜五', '这周五', '这星期五', '礼拜五', '本周五', '本星期五', '本礼拜五'})
ime.register_trigger("GetThisSaturday", "显示日期", {}, {'周六', '星期六', '礼拜六', '这周六', '这星期六', '这礼拜六', '本周六', '本星期六', '本礼拜六'})
ime.register_trigger("GetThisSunday", "显示日期", {}, {'周日', '星期日', '星期天', '礼拜日' ,'礼拜天', '这周日', '这星期日', '这星期天', '这礼拜日' ,'这礼拜天', '本周日', '本星期日', '本星期天', '本礼拜日' ,'本礼拜天'})

function GetLastMonday()
	local last, year, month, day, m, d
	last	= GetThisMonday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if day == 1 then
			if month == 3 then
				month = 2
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					day = 28
				end
			elseif month ~= 1 then
				month = month - 1
				day = _MONTH_TABLE_NORMAL[month]
			else
				month = 12
				day = 31
			end
		else
			day = day - 1
		end
	end
	return month .. "月" .. day .. "日"
end

function GetLastTuesday()
	local last, year, month, day, m, d
	last	= GetThisTuesday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if day == 1 then
			if month == 3 then
				month = 2
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					day = 28
				end
			elseif month ~= 1 then
				month = month - 1
				day = _MONTH_TABLE_NORMAL[month]
			else
				month = 12
				day = 31
			end
		else
			day = day - 1
		end
	end
	return month .. "月" .. day .. "日"
end

function GetLastWednesday()
	local last, year, month, day, m, d
	last	= GetThisWednesday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if day == 1 then
			if month == 3 then
				month = 2
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					day = 28
				end
			elseif month ~= 1 then
				month = month - 1
				day = _MONTH_TABLE_NORMAL[month]
			else
				month = 12
				day = 31
			end
		else
			day = day - 1
		end
	end
	return month .. "月" .. day .. "日"
end

function GetLastThursday()
	local last, year, month, day, m, d
	last	= GetThisThursday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if day == 1 then
			if month == 3 then
				month = 2
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					day = 28
				end
			elseif month ~= 1 then
				month = month - 1
				day = _MONTH_TABLE_NORMAL[month]
			else
				month = 12
				day = 31
			end
		else
			day = day - 1
		end
	end
	return month .. "月" .. day .. "日"
end

function GetLastFriday()
	local last, year, month, day, m, d
	last	= GetThisFriday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if day == 1 then
			if month == 3 then
				month = 2
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					day = 28
				end
			elseif month ~= 1 then
				month = month - 1
				day = _MONTH_TABLE_NORMAL[month]
			else
				month = 12
				day = 31
			end
		else
			day = day - 1
		end
	end
	return month .. "月" .. day .. "日"
end

function GetLastSaturday()
	local last, year, month, day, m, d
	last	= GetThisSaturday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if day == 1 then
			if month == 3 then
				month = 2
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					day = 28
				end
			elseif month ~= 1 then
				month = month - 1
				day = _MONTH_TABLE_NORMAL[month]
			else
				month = 12
				day = 31
			end
		else
			day = day - 1
		end
	end
	return month .. "月" .. day .. "日"
end

function GetLastSunday()
	local last, year, month, day, m, d
	last	= GetThisSunday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if day == 1 then
			if month == 3 then
				month = 2
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					day = 28
				end
			elseif month ~= 1 then
				month = month - 1
				day = _MONTH_TABLE_NORMAL[month]
			else
				month = 12
				day = 31
			end
		else
			day = day - 1
		end
	end
	return month .. "月" .. day .. "日"
end

ime.register_trigger("GetLastMonday", "显示日期", {}, {'上周一', '上星期一', '上礼拜一'})
ime.register_trigger("GetLastTuesday", "显示日期", {}, {'上周二', '上星期二', '上礼拜二'})
ime.register_trigger("GetLastWednesday", "显示日期", {}, {'上周三', '上星期三', '上礼拜三'})
ime.register_trigger("GetLastThursday", "显示日期", {}, {'上周四', '上星期四', '上礼拜四'})
ime.register_trigger("GetLastFriday", "显示日期", {}, {'上周五', '上星期五', '上礼拜五'})
ime.register_trigger("GetLastSaturday", "显示日期", {}, {'上周六', '上星期六', '上礼拜六'})
ime.register_trigger("GetLastSunday", "显示日期", {}, {'上周日', '上星期日', '上星期天', '上礼拜日', '上礼拜天'})

function GetLastMonday_1()
	local last, year, month, day, m, d
	last	= GetLastMonday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if day == 1 then
			if month == 3 then
				month = 2
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					day = 28
				end
			elseif month ~= 1 then
				month = month - 1
				day = _MONTH_TABLE_NORMAL[month]
			else
				month = 12
				day = 31
			end
		else
			day = day - 1
		end
	end
	return month .. "月" .. day .. "日"
end

function GetLastTuesday_1()
	local last, year, month, day, m, d
	last	= GetLastTuesday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if day == 1 then
			if month == 3 then
				month = 2
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					day = 28
				end
			elseif month ~= 1 then
				month = month - 1
				day = _MONTH_TABLE_NORMAL[month]
			else
				month = 12
				day = 31
			end
		else
			day = day - 1
		end
	end
	return month .. "月" .. day .. "日"
end

function GetLastWednesday_1()
	local last, year, month, day, m, d
	last	= GetLastWednesday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if day == 1 then
			if month == 3 then
				month = 2
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					day = 28
				end
			elseif month ~= 1 then
				month = month - 1
				day = _MONTH_TABLE_NORMAL[month]
			else
				month = 12
				day = 31
			end
		else
			day = day - 1
		end
	end
	return month .. "月" .. day .. "日"
end

function GetLastThursday_1()
	local last, year, month, day, m, d
	last	= GetLastThursday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if day == 1 then
			if month == 3 then
				month = 2
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					day = 28
				end
			elseif month ~= 1 then
				month = month - 1
				day = _MONTH_TABLE_NORMAL[month]
			else
				month = 12
				day = 31
			end
		else
			day = day - 1
		end
	end
	return month .. "月" .. day .. "日"
end

function GetLastFriday_1()
	local last, year, month, day, m, d
	last	= GetLastFriday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if day == 1 then
			if month == 3 then
				month = 2
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					day = 28
				end
			elseif month ~= 1 then
				month = month - 1
				day = _MONTH_TABLE_NORMAL[month]
			else
				month = 12
				day = 31
			end
		else
			day = day - 1
		end
	end
	return month .. "月" .. day .. "日"
end

function GetLastSaturday_1()
	local last, year, month, day, m, d
	last	= GetLastSaturday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if day == 1 then
			if month == 3 then
				month = 2
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					day = 28
				end
			elseif month ~= 1 then
				month = month - 1
				day = _MONTH_TABLE_NORMAL[month]
			else
				month = 12
				day = 31
			end
		else
			day = day - 1
		end
	end
	return month .. "月" .. day .. "日"
end

function GetLastSunday_1()
	local last, year, month, day, m, d
	last	= GetLastSunday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if day == 1 then
			if month == 3 then
				month = 2
				if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
					day = 29
				else
					day = 28
				end
			elseif month ~= 1 then
				month = month - 1
				day = _MONTH_TABLE_NORMAL[month]
			else
				month = 12
				day = 31
			end
		else
			day = day - 1
		end
	end
	return month .. "月" .. day .. "日"
end

ime.register_trigger("GetLastMonday_1", "显示日期", {}, {'上上周一', '上上星期一', '上上礼拜一'})
ime.register_trigger("GetLastTuesday_1", "显示日期", {}, {'上上周二', '上上星期二', '上上礼拜二'})
ime.register_trigger("GetLastWednesday_1", "显示日期", {}, {'上上周三', '上上星期三', '上上礼拜三'})
ime.register_trigger("GetLastThursday_1", "显示日期", {}, {'上上周四', '上上星期四', '上上礼拜四'})
ime.register_trigger("GetLastFriday_1", "显示日期", {}, {'上上周五', '上上星期五', '上上礼拜五'})
ime.register_trigger("GetLastSaturday_1", "显示日期", {}, {'上上周六', '上上星期六', '上上礼拜六'})
ime.register_trigger("GetLastSunday_1", "显示日期", {}, {'上上周日', '上上星期日', '上上星期天', '上上礼拜日', '上上礼拜天'})

function GetNextMonday()
	local last, year, month, day, m, d
	last	= GetThisMonday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if month == 2 and day == 28 then
			if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
				day = 29
			else
				month = month + 1
				day = 1
			end
		elseif day == _MONTH_TABLE_LEAF[month] then
			month = month + 1
			day = 1
		else
			day = day + 1	
		end
	end
	return month .. "月" .. day .. "日"
end

function GetNextTuesday()
	local last, year, month, day, m, d
	last	= GetThisTuesday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if month == 2 and day == 28 then
			if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
				day = 29
			else
				month = month + 1
				day = 1
			end
		elseif day == _MONTH_TABLE_LEAF[month] then
			month = month + 1
			day = 1
		else
			day = day + 1	
		end
	end
	return month .. "月" .. day .. "日"
end

function GetNextWednesday()
	local last, year, month, day, m, d
	last	= GetThisWednesday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if month == 2 and day == 28 then
			if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
				day = 29
			else
				month = month + 1
				day = 1
			end
		elseif day == _MONTH_TABLE_LEAF[month] then
			month = month + 1
			day = 1
		else
			day = day + 1	
		end
	end
	return month .. "月" .. day .. "日"
end

function GetNextThursday()
	local last, year, month, day, m, d
	last	= GetThisThursday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if month == 2 and day == 28 then
			if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
				day = 29
			else
				month = month + 1
				day = 1
			end
		elseif day == _MONTH_TABLE_LEAF[month] then
			month = month + 1
			day = 1
		else
			day = day + 1	
		end
	end
	return month .. "月" .. day .. "日"
end

function GetNextFriday()
	local last, year, month, day, m, d
	last	= GetThisFriday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if month == 2 and day == 28 then
			if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
				day = 29
			else
				month = month + 1
				day = 1
			end
		elseif day == _MONTH_TABLE_LEAF[month] then
			month = month + 1
			day = 1
		else
			day = day + 1	
		end
	end
	return month .. "月" .. day .. "日"
end

function GetNextSaturday()
	local last, year, month, day, m, d
	last	= GetThisSaturday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if month == 2 and day == 28 then
			if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
				day = 29
			else
				month = month + 1
				day = 1
			end
		elseif day == _MONTH_TABLE_LEAF[month] then
			month = month + 1
			day = 1
		else
			day = day + 1	
		end
	end
	return month .. "月" .. day .. "日"
end

function GetNextSunday()
	local last, year, month, day, m, d
	last	= GetThisSunday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if month == 2 and day == 28 then
			if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
				day = 29
			else
				month = month + 1
				day = 1
			end
		elseif day == _MONTH_TABLE_LEAF[month] then
			month = month + 1
			day = 1
		else
			day = day + 1	
		end
	end
	return month .. "月" .. day .. "日"
end

ime.register_trigger("GetNextMonday", "显示日期", {}, {'下周一', '下星期一', '下礼拜一'})
ime.register_trigger("GetNextTuesday", "显示日期", {}, {'下周二', '下星期二', '下礼拜二'})
ime.register_trigger("GetNextWednesday", "显示日期", {}, {'下周三', '下星期三', '下礼拜三'})
ime.register_trigger("GetNextThursday", "显示日期", {}, {'下周四', '下星期四', '下礼拜四'})
ime.register_trigger("GetNextFriday", "显示日期", {}, {'下周五', '下星期五', '下礼拜五'})
ime.register_trigger("GetNextSaturday", "显示日期", {}, {'下周六', '下星期六', '下礼拜六'})
ime.register_trigger("GetNextSunday", "显示日期", {}, {'下周日', '下星期日', '下星期天', '下礼拜日', '下礼拜天'})

function GetNextMonday_1()
	local last, year, month, day, m, d
	last	= GetNextMonday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if month == 2 and day == 28 then
			if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
				day = 29
			else
				month = month + 1
				day = 1
			end
		elseif day == _MONTH_TABLE_LEAF[month] then
			month = month + 1
			day = 1
		else
			day = day + 1	
		end
	end
	return month .. "月" .. day .. "日"
end

function GetNextTuesday_1()
	local last, year, month, day, m, d
	last	= GetNextTuesday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if month == 2 and day == 28 then
			if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
				day = 29
			else
				month = month + 1
				day = 1
			end
		elseif day == _MONTH_TABLE_LEAF[month] then
			month = month + 1
			day = 1
		else
			day = day + 1	
		end
	end
	return month .. "月" .. day .. "日"
end

function GetNextWednesday_1()
	local last, year, month, day, m, d
	last	= GetNextWednesday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if month == 2 and day == 28 then
			if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
				day = 29
			else
				month = month + 1
				day = 1
			end
		elseif day == _MONTH_TABLE_LEAF[month] then
			month = month + 1
			day = 1
		else
			day = day + 1	
		end
	end
	return month .. "月" .. day .. "日"
end

function GetNextThursday_1()
	local last, year, month, day, m, d
	last	= GetNextThursday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if month == 2 and day == 28 then
			if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
				day = 29
			else
				month = month + 1
				day = 1
			end
		elseif day == _MONTH_TABLE_LEAF[month] then
			month = month + 1
			day = 1
		else
			day = day + 1	
		end
	end
	return month .. "月" .. day .. "日"
end

function GetNextFriday_1()
	local last, year, month, day, m, d
	last	= GetNextFriday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if month == 2 and day == 28 then
			if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
				day = 29
			else
				month = month + 1
				day = 1
			end
		elseif day == _MONTH_TABLE_LEAF[month] then
			month = month + 1
			day = 1
		else
			day = day + 1	
		end
	end
	return month .. "月" .. day .. "日"
end

function GetNextSaturday_1()
	local last, year, month, day, m, d
	last	= GetNextSaturday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if month == 2 and day == 28 then
			if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
				day = 29
			else
				month = month + 1
				day = 1
			end
		elseif day == _MONTH_TABLE_LEAF[month] then
			month = month + 1
			day = 1
		else
			day = day + 1	
		end
	end
	return month .. "月" .. day .. "日"
end

function GetNextSunday_1()
	local last, year, month, day, m, d
	last	= GetNextSunday()
	m = string.find(last, "月")
	d = string.find(last, "日")
	year = os.date("%Y")
	month = tonumber(string.sub(last, 1, m - 1))
	day = tonumber(string.sub(last, m + 3, d - 1))
	local count
	for count = 1, 7 do
		if month == 2 and day == 28 then
			if year % 4 == 0 and year % 100 ~= 0 or year % 400 == 0 then
				day = 29
			else
				month = month + 1
				day = 1
			end
		elseif day == _MONTH_TABLE_LEAF[month] then
			month = month + 1
			day = 1
		else
			day = day + 1	
		end
	end
	return month .. "月" .. day .. "日"
end

ime.register_trigger("GetNextMonday_1", "显示日期", {}, {'下下周一', '下下星期一', '下下礼拜一'})
ime.register_trigger("GetNextTuesday_1", "显示日期", {}, {'下下周二', '下下星期二', '下下礼拜二'})
ime.register_trigger("GetNextWednesday_1", "显示日期", {}, {'下下周三', '下下星期三', '下下礼拜三'})
ime.register_trigger("GetNextThursday_1", "显示日期", {}, {'下下周四', '下下星期四', '下下礼拜四'})
ime.register_trigger("GetNextFriday_1", "显示日期", {}, {'下下周五', '下下星期五', '下下礼拜五'})
ime.register_trigger("GetNextSaturday_1", "显示日期", {}, {'下下周六', '下下星期六', '下下礼拜六'})
ime.register_trigger("GetNextSunday_1", "显示日期", {}, {'下下周日', '下下星期日', '下下星期天', '下下礼拜日', '下下礼拜天'})

---------------------------------------------------------------------------------------------------
