<template>
  <div class="index">
    <div class="container">
      <!-- nav -->
      <div class="box-left">
        <!-- nav -->
        <div class="top">
          <div class="top-icon">
            <i class="iconfont icon-aiji-jinzita"></i>
          </div>
          <ul class="news-item">
            <li
              v-for="item in newsItem"
              :key="item.id"
              @click="toChooiseLis(item.id)"
              :class="{'li-active': current === item.id}"
            >{{ item.name }}</li>
          </ul>
          <div class="top-txt">
            <input type="text" placeholder="search..." />
          </div>
        </div>
        <!-- 卡片资料 -->
        <div class="cards-item">
          <div class="cards-top clearfix">
            <span class="fl">Cards</span>
            <span class="fr">view all cards</span>
          </div>
          <ul>
            <li v-for="cardsItem in cards" :key="cardsItem.id">
              <span class="cards-name">{{cardsItem.name}}</span>
              <span class="cards-money">{{cardsItem.money}}</span>
              <span class="cards-number">{{ cardsItem.number }}</span>
              <span class="cards-detail">{{cardsItem.detail}}</span>
            </li>
            <li></li>
          </ul>
        </div>
        <div class="cards-info">
          <div class="cards-info-list">
            <div class="list-top clearfix">
              <span class="fl">Main Services</span>
              <span class="fr">View all</span>
            </div>
            <ul class="list-icon">
              <li v-for="iconItem in iconList" :key="iconItem.id">
                <i class="iconfont" :class="iconItem.name"></i>
                <p>{{ iconItem.txt }}</p>
              </li>
            </ul>
          </div>
          <div class="cards-info-echarts">
            <div class="info-box">
              <p class="clearfix">
                <span class="fl">Current</span>
                <span class="fr">Viewall</span>
              </p>
              <ul>
                <li class="clearfix">
                  <span>103839478349</span>
                  <span></span>
                  <span>$4,098</span>
                </li>
                <li class="clearfix">
                  <span>103839478349</span>
                  <span></span>
                  <span>$4,098</span>
                </li>
                <li class="clearfix">
                  <span>103839478349</span>
                  <span></span>
                  <span>$4,098</span>
                </li>
              </ul>
            </div>
            <div class="echarts-box">
              <p class="clearfix">
                <span class="fl">Savings</span>
                <span class="fr">Viewall</span>
              </p>
              <!-- 折线图 -->
              <div id="myChart" :style="{height: '300px'}" ref="myChart"></div>
              <ul class="show-chart-info">
                <li class="clearfix">
                  <span class="fl">Total</span>
                  <span class="fr">$100.09</span>
                </li>
                <li class="clearfix">
                  <span class="fl">This week</span>
                  <span class="fr">$2553.09</span>
                </li>
                <li class="clearfix">
                  <span class="fl">This month</span>
                  <span class="fr">$123.09</span>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
      <!-- card -->
      <div class="box-right">
        <div class="box-right-self">
          <i class="iconfont icon-jiaojuanshijianICON"></i>
          <div class="self-detail">
            <span>Admin</span>
            <img src="../assets/imgs/user.png" alt="">
          </div>
        </div>
        <div id="myPie" :style="{height: '350px'}" ref="myPie"></div>
        <ul class="pie-info">
          <li>
            <i class="iconfont icon-el-icon-shareIt"></i>
            <span>Dribbble Pro Plan</span>
            <span>-$100</span>
          </li>
          <li>
            <i class="iconfont icon-pingjunfenICON1"></i>
            <span>Adidas Refund</span>
            <span class="green">+$230</span>
          </li>
          <li>
            <i class="iconfont icon-paixuICON"></i>
            <span>Wacom LCD</span>
            <span>-$3030</span>
          </li>
        </ul>
        <div class="btn">
          <span>Transfer Money</span>
          <i class="iconfont icon-el-icon-shareIt"></i>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "index",
  props: {
    msg: String
  },
  data() {
    return {
      current: 1,
      myChart: null,
      cards: [
        {
          id: 1,
          detail: "Monzn",
          money: "$3,777",
          number: "**** **** **** *****988",
          name: "CCMP"
        },
        {
          id: 2,
          detail: "Monzn",
          money: "$2,007",
          number: "**** **** **** *****888",
          name: "CCPO"
        }
      ],
      newsItem: [
        { name: "Dashboard", id: 1 },
        { name: "Services", id: 2 },
        { name: "History", id: 3 },
        { name: "Actions", id: 4 }
      ],
      iconList: [
        { name: "icon-suoshubumenICON", txt: "Transactions", id: 1 },
        { name: "icon-zuidifenICON", txt: "Utllity", id: 2 },
        { name: "icon-jiaojuanshijianICON", txt: "Loans", id: 3 },
        { name: "icon-chakanfenxiicon", txt: "Deposits", id: 4 },
        { name: "icon-zuigaofenICON", txt: "Fast Transfer", id: 5 },
        { name: "icon-kaoshifenxiICON", txt: "Exchange", id: 6 }
      ]
    };
  },
  mounted() {
    this.drawLine();

    window.onresize = this.$echarts.init(document.getElementById("myChart")).resize;
  },
  methods: {
    toChooiseLis(id) {
      this.current = id;
    },
    drawLine() {
      // 基于准备好的dom，初始化echarts实例
      let myChart = this.$echarts.init(document.getElementById("myChart"));
      // 绘制图表
      myChart.setOption({
        xAxis: {
          type: "category",
          nameGap: 1,
          nameTextStyle: {
            color: "#959595"
          },
          axisLine: {
            show: false,
            textStyle: {
              color: "red"
            },
            lineStyle: {}
          },
          axisTick: {
            show: false
          },
          axisLabel: {
            textStyle: {
              color: "#999",
              fontSize: "12"
            }
          },
          data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
        },
        yAxis: {
          type: "value",
          nameGap: 1,
          nameTextStyle: {
            color: "#959595"
          },
          axisLine: {
            show: false,
            textStyle: {
              color: "red"
            },
            lineStyle: {}
          },
          axisTick: {
            show: false
          },
          axisLabel: {
            textStyle: {
              color: "#999",
              fontSize: "12"
            }
          }
        },
        series: [
          {
            data: [820, 932, 901, 934, 1290, 1330, 1320],
            type: "line",
            smooth: true,
            itemStyle: {
              normal: {
                color: "#4A9AA6",
                lineStyle: {
                  color: "#4A9AA6"
                }
              }
            }
          }
        ]
      });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.index {
  width: 100%;
  height: 100%;
  // background: url('../assets/imgs/login-img.png') no-repeat 100%;
  background: #fdebe8;
  padding: 80px 50px;
  box-sizing: border-box;
  .container {
    width: 100%;
    height: 100%;
    background: #fff;
    border-radius: 50px;
    border: 5px solid rgba(255, 255, 255, 0.6);
    display: flex;
    flex-direction: row;
    overflow: hidden;
    .box-left {
      flex: 1;
      height: 100%;
      // background: yellowgreen;
      .top {
        display: flex;
        padding-top: 30px;
        height: 35px;
        .top-icon {
          flex-grow: 1;
          text-align: left;
          > i {
            font-size: 30px;
            margin-left: 30px;
            color: #049bff;
          }
        }
        .news-item {
          flex-grow: 5;
          min-width: 413px;
          padding-top: 10px;
          padding-left: 95px;
          > li {
            list-style: none;
            float: left;
            color: #999;
            font-size: 16px;
            cursor: pointer;
            margin-right: 30px;
            &.li-active {
              color: #666;
            }
          }
        }
        .top-txt {
          flex-grow: 3;
          > input {
            margin-top: 10px;
            border-radius: 3px;
            border: 1px solid #999;
          }
        }
      }
      .cards-item {
        height: 180px;
        .cards-top {
          margin: 15px 0;
          margin-top: 30px;
          > span {
            &:first-child {
              margin-left: 20px;
              color: #666;
            }
            &:last-child {
              color: #999;
              margin-right: 30px;
              cursor: pointer;
            }
          }
        }
        > ul {
          display: flex;
          flex-direction: row;
          height: 140px;
          list-style: none;
          margin: 0;
          padding-right: 30px;
          box-sizing: border-box;
          > li {
            border-radius: 20px;
            height: 100%;
            background: #fff;
            flex: 1;
            margin-left: 20px;
            display: flex;
            flex-direction: column;
            text-align: left;
            padding-left: 30px;
            &:first-child {
              background: #fe4d55;
            }
            &:nth-child(2) {
              background: #0e809a;
            }
            &:last-child {
              background: #f8f8f8;
            }
            .cards-name {
              color: #666666;
              margin-top: 10px;
            }
            .cards-money {
              color: #fff;
              font-size: 18px;
              margin: 10px 0;
            }
            .cards-number {
              margin-top: 20px;
            }
            .cards-detail {
              color: #fff;
              margin-top: 10px;
            }
          }
        }
      }
      .cards-info {
        display: flex;
        flex-direction: row;
        height: calc(100% - 95px - 180px);
        overflow: hidden;
        .cards-info-list {
          padding-top: 20px;
          margin-left: 20px;
          width: 200px;
          height: 100%;
          background: #fff;
          .list-top {
            > span {
              font-size: 16px;
              &:first-child {
                color: #666;
              }
              &:last-child {
                color: #999;
                cursor: pointer;
                font-size: 14px;
              }
            }
          }
          .list-icon {
            display: flex;
            flex-direction: row;
            flex-wrap: wrap;
            margin-top: 15px;
            > li {
              width: 45%;
              margin-right: 10px;
              border-radius: 15px;
              height: 97px;
              margin-bottom: 50px;
              box-shadow: 0px 0px 10px -1px rgba(0, 0, 0, 0.5);
              padding: 22px 0;
              box-sizing: border-box;
              > i {
                color: #f997a6;
                font-size: 30px;
              }
              > p {
                margin-top: 15px;
                font-size: 12px;
              }
            }
          }
        }
        .cards-info-echarts {
          flex: 1;
          height: 100%;
          padding: 20px;
          box-sizing: border-box;
          .info-box {
            height: 30%;
            > p {
              > span {
                &:first-child {
                  color: #666;
                  font-size: 18px;
                }
                &:last-child {
                  color: #999;
                  font-size: 14px;
                  cursor: pointer;
                }
              }
            }
            > ul {
              > li {
                display: flex;
                flex-direction: row;
                margin-top: 20px;
                > span {
                  &:first-child {
                    width: 180px;
                    color: #999;
                    text-align: left;
                  }
                  &:nth-child(2) {
                    flex: 1;
                    border-bottom: 1px dashed #ededed;
                  }
                  &:last-child {
                    color: #666;
                    width: 80px;
                    text-align: right;
                  }
                }
              }
            }
          }
          .echarts-box {
            height: 70%;
            padding-top: 20px;
            box-sizing: border-box;
            > p {
              > span {
                &:first-child {
                  color: #666;
                  font-size: 18px;
                }
                &:last-child {
                  color: #999;
                  font-size: 14px;
                  cursor: pointer;
                }
              }
            }
            #myChart {
              width: 70%;
              float: left;
            }
            .show-chart-info {
              width: 30%;
              float: right;
              margin-top: 10px;
              >li{
                margin-top: 20px;
                >span{
                  &:first-child{
                    color: #999;
                  }
                  &:last-child{
                    color: #666;
                  }
                }
              }
            }
          }
        }
      }
    }
    .box-right {
      width: 280px;
      height: 100%;
      // background: gray;
      box-shadow: -28px 13px 52px -28px rgba(0, 0, 0, 0.5);
      border-radius: 50px;
      .box-right-self{
        text-align: left;
        padding-top: 40px;
        >i{
          margin-left: 20px;
          font-size: 20px;
        }
        .self-detail{
          float: right;
          margin-right: 60px;
          position: relative;
          >img{
            position: absolute;
            right: -39px;
            top: -8px;
            height: 30px;
            width: 30px;
          }
        }
      }
      #myPie{
        width: 100%;
      }
      .pie-info{
        padding-left: 20px;
        >li{
          text-align: left;
          margin-bottom: 50px;
          position: relative;
          padding-left: 60px;
          >i{
            position: absolute;
            top: -28px;
            left: -13px;
            font-size: 30px;
            color: #F95568;
            margin: 20px;
          }
          >span{
            font-size: 16px;
            &:last-child{
              color: #F95568;
              float: right;
              margin-right: 20px;
            }
            &.green{
              color: #6C9FA9;
            }
          }
        }
      }
      .btn{
        width: 100%;
        height: 42px;
        padding: 0 30px;
        box-sizing: border-box;
        text-align: left;
        position: relative;
        >span{
          display: inline-block;
          width: 100%;
          height: 100%;
          background: #FE4D55;
          line-height: 42px;
          color: #fff;
          border-radius: 25px;
          padding-left: 20px;
          cursor: pointer;
        }
        >i{
          position: absolute;
          top: 11px;
          right: 35px;
          font-size: 20px;
          color: #fff;
        }
      }
    }
  }
}
</style>
