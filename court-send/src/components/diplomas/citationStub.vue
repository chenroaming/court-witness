<template>
   <div class="box">
       <div class="header">
             <h2>福建省厦门市湖里区人民法院</h2>
             <h2>传票（存根）</h2>
         
       </div>
      <div class="main">
          <Form>
            <Row>
                <Col span="6" class="maininfo-col maininfo-col-label">
                    案号
                </Col>
                <Col span="18" class="maininfo-col">
                   <!-- <FormItem  style="width: 100%;"> -->
                        <Input v-model="backFill.caseNo"></Input>
                    <!-- </FormItem> -->
                 
                </Col>
            </Row>
            <Row>
                <Col span="6" class="maininfo-col maininfo-col-label">
                    案由
                </Col>
                <Col span="18" class="maininfo-col">
                    <!-- <FormItem  style="width: 100%;"> -->
                        <Input v-model="backFill.briefName"></Input>
                    <!-- </FormItem> -->
                </Col>
            </Row>
            <Row>
                <Col span="6" class="maininfo-col maininfo-col-label">
                    被传唤人
                </Col>
                <Col span="18" class="maininfo-col">
                    <!-- <FormItem  style="width: 100%;"> -->
                        <Input v-model="backFill.litigantName"></Input>
                    <!-- </FormItem> -->
                </Col>
            </Row>
            <Row>
                <Col span="6" class="maininfo-col maininfo-col-label">
                    住所
                </Col>
                <Col span="18" class="maininfo-col">
                    
                </Col>
            </Row>
            <Row>
                <Col span="6" class="maininfo-col maininfo-col-label">
                    传唤事由
                </Col>
                <Col span="18" class="maininfo-col">
                    <Input v-model="backFill.summonsCause"></Input>
                </Col>
            </Row>
            <Row>
                <Col span="6" class="maininfo-col maininfo-col-label">
                    应到时间
                </Col>
                <Col span="18" class="maininfo-col">
                    <!-- <FormItem  style="width: 100%;"> -->
                        <Input v-model="backFill.startDate"></Input>
                    <!-- </FormItem> -->
                </Col>
            </Row>
            <Row>
                <Col span="6" class="maininfo-col maininfo-col-label ">
                    应到处所
                </Col>
                <Col span="18" class="maininfo-col">
                    <!-- <FormItem  style="width: 100%;"> -->
                        <Input v-model="backFill.tribunalAddress"></Input>
                    <!-- </FormItem> -->
                </Col>
            </Row>
            
            <Row> 
                <Col span = "24" class="notes grid200" v-show="userCourtName == '殿前法庭'">
                    <p>备考：</p>
                </Col>
                <Col span = "24" class="notes grid200" v-show="userCourtName != '殿前法庭'">
                    <p>备考：</p>
                    <p style="margin-left:20px">
                        1.被传唤人必须准时到达应到场所；
                    </p>
                    <p style="margin-left:20px">2.本传票由被传唤人或其委托代理人携带来院报到；</p>
                    <p style="margin-left:20px">3.被传唤人收到传票后，应在送达回证上签名或盖章；</p>
                    <p style="margin-left:20px">4.当事人到本院，请携带身份证及传票。</p>
                    <p style="margin-left:20px">备注：当事人若有调解意愿，可与书记员联系。</p>
                    <p style="margin-left:20px">电话：5308405（苏晓亮）、5308400（陈艳红）。</p>
                    <p style="margin-left:20px">地址：厦门市湖里区金尚路1789号。</p>
                </Col>
                <Col span="9"push="15" class="grid200">
                        <span>法&nbsp;&nbsp;&nbsp;官:</span>
                        <FormItem>
                            <Input v-model="backFill.judgeName"></Input>
                        </FormItem><br>
                        <span>书记员:</span>
                        <FormItem>
                            <Input v-model="backFill.clerkName"></Input>
                        </FormItem>
                       
                        <p>{{backFill.noticeTime}}</p>
                        <p>（院印）</p>
                </Col>

            </Row>
           </Form>
      </div>
      <p>本联存卷</p>
   </div>

</template>

<script type="text/javascript">
import { dbList } from '@/api/diplomas.js';
export default {
    data(){
        return{
            modelHid:true,
            userCourtName:this.$store.state.app.courtName,
            title:'传票(存根)'
        }
    },
     props: {
        backFill:[Array,Object]
    },
    methods: {
        dipPro(litigantId,panelList){
            // var _this = this;
            // console.log(panelList);
            // console.log('组件调用')
                let data = {
                    litigantId:litigantId.toString(),
                    name:panelList,
                    caseNo:this.backFill.caseNo,
                    briefName:this.backFill.briefName,
                    litigantName:this.backFill.litigantName,
                    startTime:this.backFill.startTime,
                    tribunalAddress:this.backFill.tribunalAddress,
                    contactPhone:this.backFill.contactPhone,
                    judgeName:this.backFill.judgeName,
                    clerkName:this.backFill.clerkName,
                    noticeTime:this.backFill.noticeTime,
                    plaintiffName:this.backFill.plaintiffName,
                    defendantName:this.backFill.defendantName,
                    defendantNameBriefName:this.backFill.defendantNameBriefName,
                    litigantStatusName:this.backFill.litigantStatusName,
                    allMembers:this.backFill.allMembers,
                    department:this.backFill.department,
                    sendAddress:this.backFill.sendAddress,
                    sendDiploms:this.backFill.sendDiploms,
                    costMoney:this.backFill.costMoney,
                    converCaseNo:this.backFill.converCaseNo,
                    plaintiffNamePhone:this.backFill.plaintiffNamePhone,
                    defendantNamePhone:this.backFill.defendantNamePhone,
                    plaintiffLawyerNamePhone:this.backFill.plaintiffLawyerNamePhone,
                    defendantLawyerNamePhone:this.backFill.defendantLawyerNamePhone,
                    closeDate:this.backFill.closeDate,
                    converStartDate:this.backFill.converStartDate,
                    startDate:this.backFill.startDate,
                    proofPeriod:this.backFill.proofPeriod,
                    filingDate:this.backFill.filingDate,
                    type:'add',
                    summonsCause:this.backFill.summonsCause,
                }   
              dbList(
                  data
              ).then(res=>{
                //    console.log('请求成功'+JSON.stringifyres.data.state))
               if(res.data.state == 100){
                console.log('请求成功'+res)
                this.modelHid = false
                 this.$emit('model',this.modelHid,res.data.result,this.title);
               }
          }).catch(() => {
                this.$Message.error('网络错误，生成失败。');  
            });
        }
       
    }
}

</script>
<style lang="less" scoped>
  .box{
      margin: 0 auto;
      width: 700px;
      height: 100%;
      display: block;
    //   border: 1px solid black;
    font-size: 15px;
  }
  .header{
      width:100%;
      text-align: center;
  }
  .main{
      width: 100%;
      height: 100%;
      border:1px solid black;
  }
  .maininfo-col{
     border-right:1px solid black !important;
     border-bottom:1px solid black !important;
  }
 
  .maininfo-col{
      text-align: center;
  }
  .notes{
   padding: 8px;
  }
  .ivu-form-item{
      display: inline-block;
  }
    .grid200{
      height: 250px;
  }
</style>