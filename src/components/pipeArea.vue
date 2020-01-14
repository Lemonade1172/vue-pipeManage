<template>
    <div class="pipe-con">
        <div class="top-area">
            <div class="pipe-status">待审核</div>
            <div class="pipe-area">
                <div v-for='(item,index) in applyInTop'  @mousedown="MoveItem(index,'top')" class="apply-item" :key="index" ref="topItemList" :title='item.company'> {{item.company}}</div>
                <div v-for='(item,index) in applyHasPass' class="apply-item pass-item" ref="passItemList" :title='item.company'> <i class="el-icon-success"></i> {{item.company}}</div>
                <div class="pipe-line" v-for='n in totalPipe'>
                    <span class="pipe-index">{{n}}</span>
                    <span class="pipe-cell" v-for='n in 48'></span>
                </div>
            </div>
        </div>
        <div class="bottom-area" v-show='applyInBottom.length!=0'>
            <div class="pipe-status">冲突公司</div>
            <div class="pipe-area" >
                <div v-for='(item,index) in applyInBottom' @mousedown="MoveItem(index,'bottom')" class="apply-item" :key="index" ref="bottomItemList" :title='item.company'>
                    {{item.company}}
                </div>
                <div class="pipe-line" v-for='n in applyInBottom.length'>
                    <span class="pipe-index">{{n}}</span>
                    <span class="pipe-cell" v-for='n in 48'></span>
                </div>
            </div>
        </div>
        <div class="time-line">
            <span v-for='n in 25' v-show='n%2==1'>{{n-1}}:00</span>
        </div>
    </div>
</template>

<script>
    export default {
        name: "pipeArea",
        data(){
            return {
                totalPipe:12,        //总pipe数
                pipeHight:34,
                pipeInfoInit:[          //单独一个pipe内的cell信息
                        {time:'00:00',company:null},
                        {time:'00:30',company:null},
                        {time:'01:00',company:null},
                        {time:'01:30',company:null},
                        {time:'02:00',company:null},
                        {time:'02:30',company:null},
                        {time:'03:00',company:null},
                        {time:'03:30',company:null},
                        {time:'04:00',company:null},
                        {time:'04:30',company:null},
                        {time:'05:00',company:null},
                        {time:'05:30',company:null},
                        {time:'06:00',company:null},
                        {time:'06:30',company:null},
                        {time:'07:00',company:null},
                        {time:'07:30',company:null},
                        {time:'08:00',company:null},
                        {time:'08:30',company:null},
                        {time:'09:00',company:null},
                        {time:'09:30',company:null},
                        {time:'10:00',company:null},
                        {time:'10:30',company:null},
                        {time:'11:00',company:null},
                        {time:'11:30',company:null},
                        {time:'12:00',company:null},
                        {time:'12:30',company:null},
                        {time:'13:00',company:null},
                        {time:'13:30',company:null},
                        {time:'14:00',company:null},
                        {time:'14:30',company:null},
                        {time:'15:00',company:null},
                        {time:'15:30',company:null},
                        {time:'16:00',company:null},
                        {time:'16:30',company:null},
                        {time:'17:00',company:null},
                        {time:'17:30',company:null},
                        {time:'18:00',company:null},
                        {time:'18:30',company:null},
                        {time:'19:00',company:null},
                        {time:'19:30',company:null},
                        {time:'20:00',company:null},
                        {time:'20:30',company:null},
                        {time:'21:00',company:null},
                        {time:'21:30',company:null},
                        {time:'22:00',company:null},
                        {time:'22:30',company:null},
                        {time:'23:00',company:null},
                        {time:'23:30',company:null},
                    ],
                cellInfo:[],
                applyInfo:[
                    {company:'宇宙第一大合奏公司',startTime:'05:30',endTime:'10:30',half:10,pass:false},
                    {company:'站在世界中心呼唤爱公司',startTime:'09:30',endTime:'13:00',half:7,pass:false},
                    {company:'高冷王子忧郁帅哥公司',startTime:'07:30',endTime:'11:30',half:8,pass:false},
                    {company:'大脑当机公司',startTime:'06:30',endTime:'11:30',half:10,pass:false},
                    {company:'玛丽学院公司',startTime:'12:30',endTime:'16:30',half:8,pass:false},   
                    {company:'浪子回头公司',startTime:'18:30',endTime:'20:30',half:4,pass:false},
                    {company:'亲爱的无情孙小美公司',startTime:'10:30',endTime:'16:30',half:12,pass:false},
                    {company:'阿土伯合资公司',startTime:'12:30',endTime:'16:30',half:8,pass:false},
                    {company:'声声慢合资集团',startTime:'04:30',endTime:'16:30',half:24,pass:false},
                    {company:'齐桓公公司',startTime:'06:30',endTime:'13:30',half:14,pass:false},
                    {company:'鲁庄公公司',startTime:'06:30',endTime:'15:30',half:18,pass:false},
                    {company:'宇宙第一大合奏公司',startTime:'05:30',endTime:'10:30',half:10,pass:false},
                    {company:'站在世界中心呼唤爱公司',startTime:'09:30',endTime:'13:00',half:7,pass:false},
                    {company:'高冷王子忧郁帅哥公司',startTime:'07:30',endTime:'11:30',half:8,pass:false},
                    {company:'大脑当机公司',startTime:'06:30',endTime:'11:30',half:10,pass:false},
                    {company:'玛丽学院公司',startTime:'12:30',endTime:'16:30',half:8,pass:false},
                    {company:'浪子回头公司',startTime:'18:30',endTime:'20:30',half:4,pass:false},
                    {company:'亲爱的无情孙小美公司',startTime:'10:30',endTime:'16:30',half:12,pass:false},
                    {company:'阿土伯合资公司',startTime:'12:30',endTime:'16:30',half:8,pass:false},
                    {company:'声声慢合资集团',startTime:'04:30',endTime:'16:30',half:24,pass:false},
                    {company:'齐桓公公司',startTime:'06:30',endTime:'13:30',half:14,pass:false},
                    {company:'鲁庄公公司',startTime:'06:30',endTime:'15:30',half:18,pass:false},
                ],
                applyHasPass:[
                    {company:'玩味末日颓废公司',startTime:'02:30',endTime:'06:00',half:7,pass:true,pipeIndex:0},
                    {company:'圆舞曲爱人公司',startTime:'15:30',endTime:'18:00',half:5,pass:true,pipeIndex:1},
                ],
                applyInTop:[],      //待审核区域的申请信息
                applyInBottom:[],   //冲突区域的申请信息
            }
        },
        mounted(){
            this.InitCellInfo();
            this.RenderPassApply();
            this.WhoIsTop();
        },
        updated(){
            this.RenderApply();
        },
        methods:{
             //自动排序将请求渲染到对应位置
             RenderApply(){
                let halfHourWidth = 18;         //半小时宽度为16+2px边框 => 18px
                let pipeHight = 34;             //一个通道的高度为32+2px => 34px
                let indexCellWidth = 34+20-1;        //每个通道index的宽度 + pipeArea的padding - 1px留给每个申请box绘制的左border
                for(let index in this.applyInTop){      //渲染待审核申请
                let item = this.applyInTop[index];          //ref名相同时会自动归到一个数组中
                    this.$refs.topItemList[index].style.top = pipeHight*item.pipeIndex + 'px';
                    this.$refs.topItemList[index].style.width = halfHourWidth*item.half - 6*2 +'px'; //减去padding6*2
                    this.$refs.topItemList[index].style.left = indexCellWidth + halfHourWidth*item.startCell  + 'px';
                }
                for(let index in this.applyInBottom){      //渲染待审核申请
                let item = this.applyInBottom[index];
                    this.$refs.bottomItemList[index].style.top = pipeHight*index + 'px';
                    this.$refs.bottomItemList[index].style.width = halfHourWidth*item.half - 6*2 +'px'; //减去padding6*2
                    this.$refs.bottomItemList[index].style.left = indexCellWidth + halfHourWidth*item.startCell  + 'px';
                }
            },
            //拖动排序  上方申请提起又放在原来位置的需要特殊处理
            // 通道上的申请公司有三种情况
            // 有，并且已经被审核，不能替换，回到原位置√
            // 有，（1~n个）初始排序后的同等级申请， 替换。
            // 没有（第一次拖动所有通道该位置不出现空缺，只有二次及以上才会出现该情况，即原始自动排序顺序被打乱），将该申请移动到上方数组中，并标记好通道数
            MoveItem(index,type){
                let event = window.event;
                let odiv = event.target;    //获取目标元素
                odiv.style.background = '#57647C';              //样式的变换不能用数据判断直接替换css类的方法，在切换的时候，位置信息的设置会失效
                odiv.style.color = 'white';
                odiv.style.zIndex = '99';
                let disY = event.clientY - odiv.offsetTop;  //鼠标相对元素的位置
                let top = 0;            //拖动的位置
                if(type=='bottom'){     //拖动冲突区域申请
                    let item = this.applyInBottom[index];
                    document.onmousemove = (e) => {    //鼠标按下并移动的事件
                        top = e.clientY - disY;             //用鼠标的位置减去鼠标相对元素的位置，得到元素的位置
                        let topLimited = 34*this.totalPipe + 5;
                        let bottomLimited = 34*(this.applyInBottom.length-1);
                        if (top < -topLimited) {        //移动当前元素超过边界时的控制
                            top = -topLimited;
                        } else if (top > bottomLimited) {
                            top = bottomLimited;
                        }
                        odiv.style.top = top + 'px';
                    };
                    document.onmouseup = (e) => {
                        odiv.style.background = '#ADBCD5';
                        odiv.style.color = '#333';
                        odiv.style.zIndex = '1';
                        if(top>-5){                      //只是在冲突区域拖动，回到原来位置
                            odiv.style.top = this.pipeHight*index + 'px';
                        }else{                          //拖动到上方
                            let downPipeIndex = this.GetDownPipeIndex(top,'bottom');
                            let pipeNow = this.cellInfo[downPipeIndex];
                            let canDrop = this.IsDragCanDown(item,pipeNow);
                            if(!canDrop){               //不能放下，回到原来位置
                                odiv.style.top = this.pipeHight*index + 'px';
                            }else{                      //能放下，进行替换操作
                                item.pipeIndex = downPipeIndex;         //记录放下的通道
                                let cellIndex = pipeNow.findIndex((cell)=>cell.time == item.startTime);
                                if(this.IsPipeAvailable(item,pipeNow)){       //能直接放下
                                    this.ChangeItem2Top(item);
                                    for(let n = 0;n < item.half;n++){
                                        pipeNow[cellIndex+n].company = item;    //记录占用公司信息,将当前通道上该申请的时间段设为被占用
                                    }
                                }else{      //需要替换
                                    this.ReplaceOldByDrop(item,pipeNow);
                                }
                            }
                        }   
                        document.onmousemove = null;
                        document.onmouseup = null;
                        console.log(this.applyInTop);
                        console.log(this.applyInBottom);
                    };
                }else{          //待审核区域的拖动
                    let item = this.applyInTop[index];
                    document.onmousemove = (e) => {    //鼠标按下并移动的事件
                        top = e.clientY - disY;             //用鼠标的位置减去鼠标相对元素的位置，得到元素的位置
                        let bottomLimited = 34*(this.applyInBottom.length-1+this.totalPipe)+5;
                        if (top < 0) {        //移动当前元素超过边界时的控制
                            top = 0;
                        } else if (top > bottomLimited) {
                            top = bottomLimited;
                        }
                        odiv.style.top = top + 'px';
                    };
                    document.onmouseup = (e) => {
                        odiv.style.background = '#ADBCD5';
                        odiv.style.color = '#333';
                        odiv.style.zIndex = '1';
                        let centerBorder = 34*(this.totalPipe-1)+34/2;
                        if(top > centerBorder){ //拖动到冲突区
                            let topSet = new Set([...this.applyInTop]);
                            let dragSet = new Set([...[item]]);
                            this.applyInTop = Array.from(new Set([...topSet].filter(item => !dragSet.has(item))));    //从top数组删除拖动的item
                            this.applyInBottom = this.applyInBottom.concat([item]);    
                            let pipeNow = this.cellInfo[item.pipeIndex];
                            this.ClearPipeOld([item],pipeNow);                              
                        }else{          //在待审核区域拖动
                            let downPipeIndex = this.GetDownPipeIndex(top,'top');
                            let pipeNow = this.cellInfo[downPipeIndex];
                            let canDrop = this.IsDragCanDown(item,pipeNow);
                            if(!canDrop){               //不能放下，回到原来位置
                                odiv.style.top = this.pipeHight*item.pipeIndex + 'px';
                            }else{                      //能放下，直接放下或者放下并进行替换操作
                                this.ClearPipeOld([item],this.cellInfo[item.pipeIndex]);    //清除原通道记录信息                              
                                item.pipeIndex = downPipeIndex;         //记录放下的通道
                                let cellIndex = pipeNow.findIndex((cell)=>cell.time == item.startTime);
                                if(this.IsPipeAvailable(item,pipeNow)){       //能直接放下
                                    this.RenderApply();
                                    for(let n = 0;n < item.half;n++){
                                        pipeNow[cellIndex+n].company = item;    //记录占用公司信息,将当前通道上该申请的时间段设为被占用
                                    }
                                }else{      //需要替换
                                    this.ReplaceOldByDrop(item,pipeNow);
                                }
                            }
                        }
                        document.onmousemove = null;
                        document.onmouseup = null;
                console.log(this.applyInTop);
                console.log(this.applyInBottom);
                    };
                }
            },
            //将申请从下方数组挪到上方数组
            ChangeItem2Top(item){
                let bottomSet = new Set([...this.applyInBottom]);
                let dragSet = new Set([...[item]]);
                this.applyInBottom = Array.from(new Set([...bottomSet].filter(item => !dragSet.has(item))));    //从bottom数组删除被替换的item
                this.applyInTop = [item].concat(this.applyInTop);   //优先排序被拖动申请
            },
            //判断手动排序放下时的通道位置
            GetDownPipeIndex(top,type){
                let downPipeIndex = 0;
                let pipeCalcHeight = 0;
                type == 'bottom'?pipeCalcHeight = top+34*this.totalPipe + 5:pipeCalcHeight = top;
                downPipeIndex = pipeCalcHeight/34;
                downPipeIndex = Math.round(downPipeIndex);      //吸附到更接近的通道
                return downPipeIndex;
            },
            //拖动排序替换操作
            ReplaceOldByDrop(apply,pipeNow){
                let oldApply = [];                  //记录需要被替换的申请 
                for(let cellIndex in pipeNow){                      
                    if(pipeNow[cellIndex].time == apply.startTime){        //在当前通道找到申请开始时间的cellIndex
                        for(let n = 0; n < apply.half; n++){
                            let index = Number(cellIndex) + n;
                            if(pipeNow[index].company){      //该通道在申请时间段内有格子被占用,记录该占用公司
                                oldApply.push(pipeNow[index].company);
                            }
                        }
                        oldApply = Array.from(new Set([...oldApply]));      //去重
                        if(oldApply[0]==apply){         //待审核区域申请提起又放在原来位置时的特殊处理，直接放在原位置
                            this.RenderApply();
                            return;
                        }
                        this.ClearPipeOld(oldApply,pipeNow);
                        for(let n = 0; n < apply.half; n++){
                            let index = Number(cellIndex) + n;
                            pipeNow[index].company = apply;
                        }
                        oldApply.map(item=>{
                            item.pipeIndex = '';
                        })
                    }
                }
                let topSet = new Set([...this.applyInTop]);
                let bottomSet = new Set([...this.applyInBottom]);
                let oldSet = new Set([...oldApply]);
                let dragSet = new Set([...[apply]]);
                this.applyInTop = Array.from(new Set([...topSet].filter(item => !oldSet.has(item))));    //从top数组删除被替换的item
                this.applyInTop = [apply].concat(this.applyInTop);                                  //优先绘制拖动item
                this.applyInBottom = Array.from(new Set([...bottomSet].filter(item => !dragSet.has(item))));    //从bottom数组删除被替换的item
                this.applyInBottom = this.applyInBottom.concat(oldApply);
            },
            //清除通道上被替换申请的信息
            ClearPipeOld(oldApply,pipeNow){
                oldApply.map(item=>{
                    for(let cellIndex in pipeNow){
                        if(pipeNow[cellIndex].time == item.startTime){
                            for(let n = 0; n < item.half; n++){
                                let index = Number(cellIndex) + n;
                                pipeNow[index].company=null;
                            }
                        }
                    }
                });
            },
            //根据拿到的通道数，每个通道初始化48个小格子，带有时间信息和占用状态。(二维数组)
            InitCellInfo(){
                for(let i = 0;i<this.totalPipe;i++){
                    let pipeInfo = JSON.parse(JSON.stringify(this.pipeInfoInit));
                    this.cellInfo.push(pipeInfo);
                }
            },
            // 将后台返回的已审核申请绘制在表格中
            RenderPassApply(){
                this.applyHasPass.map(item=>{
                    let pipeNow = this.cellInfo[item.pipeIndex];             //记录当前通道
                    let cellIndex = pipeNow.findIndex((cell)=>cell.time == item.startTime);
                    item['startCell'] = cellIndex;              //记录绘制时的cell位置
                    for(let n = 0;n < item.half;n++){
                        pipeNow[cellIndex+n].company = item;    //记录占用公司,将当前通道上该申请的时间段设为被占用
                     }
                });
                let halfHourWidth = 18;         //半小时宽度为16+2px边框 => 18px
                let pipeHight = 34;             //一个通道的高度为32+2px => 34px
                let indexCellWidth = 34+20-1;        //每个通道index的宽度 + pipeArea的padding - 1px留给每个申请box绘制的左border
                for(let index in this.applyHasPass){      //渲染待审核申请
                let item = this.applyHasPass[index];          //ref名相同时会自动归到一个数组中
                    this.$refs.passItemList[index].style.top = pipeHight*item.pipeIndex + 'px';
                    this.$refs.passItemList[index].style.width = halfHourWidth*item.half - 6*2 + 'px'; //减去padding6*2
                    this.$refs.passItemList[index].style.left = indexCellWidth + halfHourWidth*item.startCell  + 'px';
                }
            },
            //进入页面获取数据后,根据给出的通道数和申请信息做计算，区分出排在待审核区域的申请数组和排在冲突区域的申请数组,并给通道中的被占用cell做出标记
            WhoIsTop(){
                this.applyInfo.map(item=>{                              //遍历申请列表
                    for(let pipeIndex in this.cellInfo){                //遍历通道
                        let pipeNow = this.cellInfo[pipeIndex];             //记录当前通道
                        let cellIndex = pipeNow.findIndex((cell)=>cell.time == item.startTime);
                        item['startCell'] = cellIndex;              //记录绘制时的cell位置
                        if(this.IsPipeAvailable(item,pipeNow)){
                            for(let n = 0;n < item.half;n++){
                                pipeNow[cellIndex+n].company = item;    //记录占用公司信息,将当前通道上该申请的时间段设为被占用
                            }
                            item['pipeIndex'] = pipeIndex;              //记录该申请放置的通道
                            this.applyInTop.push(item);                 //将该申请存放入待审核数组
                            break;
                        }
                    }
                });
                let topSet = new Set([...this.applyInTop]);
                let allSet = new Set([...this.applyInfo]);
                let bottomSet = new Set([...allSet].filter(item => !topSet.has(item)));
                this.applyInBottom = Array.from(bottomSet)
            },
            //手动排序时申请在一个通道能否放置
            IsDragCanDown(apply,pipeNow){     //遍历拖动申请在该通道上需要占用的cell信息，根据该段cell记录的信息（是否被占用，以及被占用的申请的状态）
                let canPut = true;
                for(let cellIndex in pipeNow){                      
                    if(pipeNow[cellIndex].time == apply.startTime){        //在当前通道找到申请开始时间的cellIndex
                        for(let n = 0; n < apply.half; n++){
                            let index = Number(cellIndex) + n;
                            if(pipeNow[index].company!=null&&pipeNow[index].company.pass){      //该通道在申请时间段内有格子被占用并且该占用申请为审核通过状态
                                canPut = false; 
                                break;
                            }        
                        }
                    }
                }
                return canPut;
            },
            //申请自动排序时在一个通道是否可放置
            IsPipeAvailable(apply,pipeNow){
                let canPut = true;
                for(let cellIndex in pipeNow){                      
                    if(pipeNow[cellIndex].time == apply.startTime){        //在当前通道找到申请开始时间
                        if(!pipeNow[cellIndex].company){               //若当前通道上该申请开始时间可用（需要开始时间之后到结束时间之前的每一个格子都可用）
                            for(let n = 0; n < apply.half; n++){
                                let index = Number(cellIndex) + n;
                                if(pipeNow[index].company){      //该通道在申请时间段内有格子被占用
                                    canPut = false; 
                                    break;
                                }        
                            }
                        }else{                              //若当前通道上该申请开始时间不可用
                            canPut = false;     
                        }
                    }
                }
                return canPut;
            },
        }
    }
</script>

<style scoped>
    .time-line{
        display: flex;
        margin-left: 80px;
    }
    .time-line span{
        width: 71px;
        margin-right: 1px;
        color: #A6ACBB;
        font-size: 12px;
    }
    .apply-item{
        cursor: pointer;
        user-select: none;
        position: absolute;
        padding: 0 6px;
        height: 32px;
        line-height: 32px;
        background: #ADBCD5;
        border: 1px solid #E4E4E4;
        overflow: hidden;
        text-overflow:ellipsis;
        white-space: nowrap;
    }
    .pass-item{
        background: #09C670;
        border: 1px solid #E4E4E4;
        color: #079253;
    }
    .pipe-area{
        position: relative;
        background: white;
        padding-left: 20px;
    }
    .top-area,.bottom-area{
        display: flex;
        align-items: center;
        background: #E9EEF5;
        width: 960px;
    }
    .bottom-area{
        border-top:5px solid #C4C7CC ;
    }
    .pipe-status{
        width: 25px;
        padding: 0 12px 0 12px;
    }
    .pipe-line{
        display: flex;
        flex-wrap: nowrap;
        align-items: center;
    }
    .pipe-index{
        line-height: 32px;
        height: 32px;
        width: 32px;
        text-align: center;
        border: 1px solid #E4E4E4;
    }
    .pipe-cell{
        height: 32px;
        width: 16px;
        border: 1px solid #E4E4E4;
    }
    .top-area .pipe-index{
        background: #E9EEF5;
    }
    .top-area .pipe-cell{
        background: #F6F7F9;
    }
    .bottom-area .pipe-index{
        background: #F7EFF0;
    }
    .bottom-area .pipe-cell{
        background: #F7EFF0;
    }
</style>