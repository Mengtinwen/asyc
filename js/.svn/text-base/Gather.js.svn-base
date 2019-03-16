(function (mui,owner){
	var nowTime = "";
	var CountDownJson = JsonTime = {};										   			//时间类型Json
		
	/**
	 * 获取系统当前时间Json
	 * 使用方法通过调用getTime()函数 . 所需要的时间类型。例：getTime().value;即获得年月日时分秒的时间类型
	 * "说明：":"变量对应时间说明。",
	 * "Y":"年","M":"月","D":"日","h":"时","m":"分","s":"秒","Year":"年月日",
	 * "Month":"月日","Hours":"时分","Minutes":"分秒","HM":"时分秒","value":"年月日时分秒","text":"月日时分",
	 * "Dy":"星期","timestamp":"时间戳（从1970-1-1 00:00:00）到当前时间的毫秒数"
	 */
	owner.getTime = function(Times){
		nowTime = (Times == undefined) ? new Date() : new Date(Times);      //获取时间对象
		JsonTime.Y = nowTime.getFullYear();									//年
		JsonTime.M = nowTime.getMonth()+1;									//月
		JsonTime.D = nowTime.getDate();										//日
		JsonTime.h = Gather.checkTime(nowTime.getHours());					//时
		JsonTime.m = Gather.checkTime(nowTime.getMinutes());				//分
		JsonTime.s = Gather.checkTime(nowTime.getSeconds());				//秒
		JsonTime.Year = JsonTime.Y+"-"+JsonTime.M+"-"+JsonTime.D;			//年月日
		JsonTime.Yearc = JsonTime.Y+"年"+JsonTime.M+"月"+JsonTime.D+"日";	//年月日
		JsonTime.Month = JsonTime.M+"-"+JsonTime.D;							//月日
		JsonTime.Monthc = JsonTime.M+"月"+JsonTime.D+"日";					//月日
		JsonTime.Hours = JsonTime.h+":"+JsonTime.m;							//时分
		JsonTime.Hourc = JsonTime.h+"时"+JsonTime.m+"分";					//时分
		JsonTime.Minutes = JsonTime.m+":"+JsonTime.s;						//分秒
		JsonTime.Minutec = JsonTime.m+"分"+JsonTime.s+"秒";					//分秒
		JsonTime.HM = JsonTime.h+":"+JsonTime.m+":"+JsonTime.s;				//时分秒
		JsonTime.HMc = JsonTime.h+"时"+JsonTime.m+"分"+JsonTime.s+"秒";		//时分秒
		JsonTime.value =JsonTime.Year+" "+JsonTime.HM;						//年月日时分秒
		JsonTime.text = JsonTime.Month+" "+JsonTime.Hours;					//月日时分
		JsonTime.Dy = owner.getDY(nowTime.getDay());						//星期
		JsonTime.timestamp = nowTime.getTime();								//时间戳
		JsonTime.valueText =JsonTime.Yearc+" "+JsonTime.Dy+" "+JsonTime.HMc; //年月日时分秒
		
		return JsonTime;
	}
	
	/**
	 * 获取星期
	 * @param {Number} 传递星期数值;
	 * @param {String} 星期格式，可取以数组类型。传递week 为星期* 格式;默认为 weeks 周几
	 * 星期从0 到 6，0为星期天、
	 */
	owner.getDY = function(days,type){
		var weeks = ['周日','周一','周二','周三','周四','周五','周六'];
		var week  = ['星期天','星期一','星期二','星期三','星期四','星期五','星期六'];
		var liBai = ['礼拜天','礼拜一','礼拜二','礼拜三','礼拜四','礼拜五','礼拜六'];
		var str = "";
		if(type == "week"){
			Arr = week;
		}else if(type == "liBai"){
			Arr = liBai;
		}else{
			Arr = weeks;
		}
		
		switch(days){
			case 0:
				str = Arr[0];
			    break;
			case 1:
				str =  Arr[1];
			    break;
			case 2:
				str =  Arr[2];
			    break;
			case 3:
				str =  Arr[3];
			    break;
			case 4:
				str =  Arr[4];
			    break;
			case 5:
				str =  Arr[5];
			    break;
			case 6:
				str =  Arr[6];
			    break;
		}
		return str;
	}
	
	/**
	 * 倒计时获取 天 时 分 秒
	 * @param {String} year 目标时间
	 * @param {String} divname Dom ID 名
	 * @param {Boolean} Bool 参数true 为自身调用;不传或空则需要外部写setInterval
	 **/
	owner.ShowCountDown = function(year,divname,Bool){
        var now = new Date();
        endDate = year.replace(/\-/g, "\/"); 						//替换字符，变成标准格式  
        endDate = new Date(Date.parse(endDate));					//转换为中国标准时间  Tue Feb 05 2019 00:00:00 GMT+0800 (中国标准时间)
        CountDownJson.D = parseInt((endDate - now) / 1000 / 3600 / 24, 10);	//计算剩余的天数
        CountDownJson.H = Gather.checkTime(parseInt((endDate - now) / 1000 / 3600 % 24, 10));	//计算剩余的小时数
        CountDownJson.M = Gather.checkTime(parseInt((endDate - now) / 1000 / 60 % 60, 10));	//计算剩余的分钟数
        CountDownJson.S = Gather.checkTime(parseInt((endDate - now) / 1000 % 60, 10));			//计算剩余的秒数
		CountDownJson.value = CountDownJson.D + " 天 " + CountDownJson.H + " 小时 " + CountDownJson.M + " 分 " + CountDownJson.S + " 秒";
        
		var cc = document.getElementById(divname);
        cc.innerHTML =  CountDownJson.value;
		
        if(Bool){setInterval(function(){owner.ShowCountDown(year,divname);}, 1000);}
		
		return CountDownJson;
    }
	
	/**
	 * 小于10 在前加个0
	 */
	Gather.checkTime = function(i){
		return (i < 10 ) ? ("0" + i) : i;
	}
	
	/**
	 * 获取当前日期前后的时间天数
	 * @param {Object} cheDate 目标时间的以前时间天数
	 * @param {Object} num     天数，设置参数可获取天数，例：设置2019-1-25，10 则当前设置日期的前十天
	 * @param {Object} type	   加、减号  + 为指定日期后的天数，- 为指定日期前的天数
	 */
	owner.getOldTime = function(cheDate,num,type){
		var oldDate = [];
		var day = 3600*24*1000;										//计算一天的毫秒数
		var numbers = num || 1;
		if(cheDate != "" && cheDate != undefined){
			datem = new Date(Date.parse(cheDate))
		}else{
			datem = new Date();										//获取当前时间
		}
		
   		oldDate.push({
			time:owner.getDY(datem.getDay()),					    //获取星期
			day:(datem.getMonth()+1)+" / "+datem.getDate(),			//获取月日
			value:datem,
   		})
   		
	    for(var i = 0;i<numbers;i++){								//循环获取当前日期的前五天
	    	if(type == "+"){
	    		timess = datem.getTime() + day*(i+1);				//当时日期毫秒数加每天的毫秒数循环加五天
	    	}else{
	    		timess = datem.getTime() - day*(i+1);				//当时日期毫秒数减去每天的毫秒数循环减五天
	    	}
	   		times = new Date(timess);								//毫秒转换成中国标准时间
	   		oldDate.push({
   				time:owner.getDY(times.getDay()),					//获取星期
   				day:(times.getMonth()+1)+" / "+times.getDate(),		//获取月日
   				value:times,
	   		})
	    }
	    return oldDate;
	}
	
	Gather.countDown = function(minute){
		var minute = minute-1;
		var second = 59;
		var countDowns = {}
		setInterval(function(){
			if(second >= 0){
				second-=1;
				if(second < 10){
					second = Gather.checkTime(second)
					if(second == "0-1"){
						minute -=1;
						second = 59;
					}
				}
			}
			
			countDowns.minute = minute;
			countDowns.second = second;
			countDowns.value = minute+":"+second;
			
			console.log(countDowns)
			return countDowns;
		},1000)
		
	}
	
	
	/**
	 * 分秒倒计时
	 * @param {Object} maxtime
	 * @param {Object} DomId
	 */
    Gather.CountDown = function(maxtime,DomId) {
    	var maxtime = maxtime * 60; //一个小时，按秒计算，自己调整!   
        
        timer = setInterval(function(){
        	if (maxtime >= 0) {
	            minutes = Math.floor(maxtime / 60);
	            seconds = Math.floor(maxtime % 60);
	            msg = Gather.checkTime(minutes) + ":" + Gather.checkTime(seconds);
	            document.getElementById(DomId).innerHTML = msg;
	            if (maxtime == 5 * 60)mui.toast("距离考试结束还剩5分钟");
	            --maxtime;
	         } else{
	            clearInterval(timer);
	            return "true"
	        }
        }, 1000);
    }
    
	
}(mui,window.Gather = {}))