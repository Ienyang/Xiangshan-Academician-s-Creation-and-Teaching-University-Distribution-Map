<template>
  <div class="university-map-container">
    <div id="map-chart" style="width: 100%; height: 1000px;"></div>
  </div>
</template>

<script>
import * as echarts from 'echarts'

export default {
  name: 'UniversityMap',
  data() {
    return {
      universities: [
        {
          name: '清华学校',
          location: [116.32, 40.00],
          value: 100,
          category: 0,
          relationships: [
            { person: '唐国安', relationship: '任教', time: '1911-1913' },
            { person: '唐悦良', relationship: '任教', time: '1911-1913' },
            { person: '唐绪一', relationship: '任教', time: '1928-1937' }
          ]
        },
        {
          name: '北洋大学堂',
          location: [117.17, 39.08],
          value: 85,
          category: 0,
          relationships: [
            { person: '梁如浩', relationship: '任教', time: '1900-1902' },
            { person: '唐绍仪', relationship: '任教', time: '1895-1897' }
          ]
        },
        {
          name: '山东大学堂',
          location: [117.05, 36.67],
          value: 80,
          category: 0,
          relationships: [
            { person: '唐绍仪', relationship: '任教', time: '1901-1902' },
            { person: '韦悫', relationship: '任教', time: '1928-1930' }
          ]
        },
        {
          name: '复旦大学',
          location: [121.51, 31.30],
          value: 95,
          category: 0,
          relationships: [
            { person: '唐绍仪', relationship: '任教', time: '1912-1913' },
            { person: '唐元湛', relationship: '任教', time: '1920-1922' },
            { person: '薛仙舟', relationship: '任教', time: '1920-1922' }
          ]
        },
        {
          name: '国立音乐院',
          location: [121.47, 31.23],
          value: 75,
          category: 1,
          relationships: [
            { person: '萧友梅', relationship: '创办', time: '1927' },
            { person: '萧友梅', relationship: '任教', time: '1927-1940' }
          ]
        },
        {
          name: '华中大学',
          location: [114.37, 30.52],
          value: 80,
          category: 0,
          relationships: [
            { person: '韦卓民', relationship: '任教', time: '1924-1951' }
          ]
        },
        {
          name: '格致书院',
          location: [121.48, 31.22],
          value: 60,
          category: 2,
          relationships: [
            { person: '唐廷枢', relationship: '创办', time: '1874' },
            { person: '唐廷桂', relationship: '任职', time: '1877' }
          ]
        },
        {
          name: '唐山路矿学堂',
          location: [104.06, 30.67],
          value: 80,
          category: 0,
          relationships: [
            { person: '梁如浩', relationship: '任教', time: '1896-1900' }
          ]
        },
        {
          name: '黄埔军校',
          location: [113.45, 23.10],
          value: 90,
          category: 3,
          relationships: [
            { person: '孙中山', relationship: '创办', time: '1924' }
          ]
        },
        {
          name: '广东农事试验场',
          location: [113.35, 23.15],
          value: 75,
          category: 0,
          relationships: [
            { person: '唐有恒', relationship: '创办', time: '1908' },
            { person: '唐有恒', relationship: '任教', time: '1908-1920' }
          ]
        },
        {
          name: '中山大学',
          location: [113.29, 23.13],
          value: 90,
          category: 0,
          relationships: [
            { person: '孙中山', relationship: '创办', time: '1924' }
          ]
        },
        {
          name: '岭南大学',
          location: [113.27, 23.13],
          value: 70,
          category: 0,
          relationships: [
            { person: '钟荣光', relationship: '任教', time: '1915-1951' }
          ]
        },
        {
          name: '燕京大学',
          location: [116.31, 39.99],
          value: 85,
          category: 0,
          relationships: [
            { person: '唐悦良', relationship: '任教', time: '1920-1922' }
          ]
        },
        {
          name: '江淮大学',
          location: [118.78, 32.07],
          value: 75,
          category: 0,
          relationships: [
            { person: '韦悫', relationship: '任教', time: '1942-1944' }
          ]
        },
        {
          name: '华东大学',
          location: [117.05, 36.67],
          value: 75,
          category: 0,
          relationships: [
            { person: '韦悫', relationship: '任教', time: '1928-1930' }
          ]
        }
      ],
      professors: [
        {
          name: '唐绍仪',
          color: '#FF6B6B',
          universities: [
            { name: '山东大学堂', location: [117.05, 36.67], tenure: '1901-1902' },
            { name: '北洋大学堂', location: [117.17, 39.08], tenure: '1895-1897' },
            { name: '复旦大学', location: [121.51, 31.30], tenure: '1912-1913' }
          ]
        },
        {
          name: '梁如浩',
          color: '#4ECDC4',
          universities: [
            { name: '唐山路矿学堂', location: [104.06, 30.67], tenure: '1896-1900' },
            { name: '北洋大学堂', location: [117.17, 39.08], tenure: '1900-1902' }
          ]
        },
        {
          name: '唐有恒',
          color: '#45B7D1',
          universities: [
            { name: '广东农事试验场', location: [113.35, 23.15], tenure: '1908-1920' }
          ]
        },
        {
          name: '唐国安',
          color: '#96CEB4',
          universities: [
            { name: '清华学校', location: [116.32, 40.00], tenure: '1911-1913' }
          ]
        },
        {
          name: '钟荣光',
          color: '#FFEEAD',
          universities: [
            { name: '岭南大学', location: [113.27, 23.13], tenure: '1915-1951' }
          ]
        },
        {
          name: '韦卓民',
          color: '#D4A5A5',
          universities: [
            { name: '华中大学', location: [114.37, 30.52], tenure: '1924-1951' }
          ]
        },
        {
          name: '萧友梅',
          color: '#9B59B6',
          universities: [
            { name: '国立音乐院', location: [121.47, 31.23], tenure: '1927-1940' }
          ]
        },
        {
          name: '韦悫',
          color: '#3498DB',
          universities: [
            { name: '山东大学堂', location: [117.05, 36.67], tenure: '1928-1930' },
            { name: '江淮大学', location: [118.78, 32.07], tenure: '1942-1944' }
          ]
        },
        {
          name: '唐元湛',
          color: '#2ECC71',
          universities: [
            { name: '复旦大学', location: [121.51, 31.30], tenure: '1920-1922' }
          ]
        },
        {
          name: '唐悦良',
          color: '#F1C40F',
          universities: [
            { name: '清华学校', location: [116.32, 40.00], tenure: '1911-1913' },
            { name: '燕京大学', location: [116.31, 39.99], tenure: '1920-1922' }
          ]
        },
        {
          name: '唐绪一',
          color: '#E74C3C',
          universities: [
            { name: '清华学校', location: [116.32, 40.00], tenure: '1928-1937' }
          ]
        },
        {
          name: '薛仙舟',
          color: '#8E44AD',
          universities: [
            { name: '复旦大学', location: [121.51, 31.30], tenure: '1920-1922' }
          ]
        }
      ]
    }
  },
  mounted() {
    this.loadMap()
  },
  methods: {
    async loadMap() {
      const chinaMap = await fetch('https://geo.datav.aliyun.com/areas_v3/bound/100000_full.json')
        .then(response => response.json())
      echarts.registerMap('china', chinaMap)
      this.initMapChart()
    },
    initMapChart() {
      const mapChart = echarts.init(document.getElementById('map-chart'))

      // 定义放大气泡区域
      const bubbleRegions = [
        {
          name: '北京地区',
          center: [116.32, 39.95],
          radius: 80, // 较小的气泡
          direction: 'rightBottom', // 向右下方引出，偏30度
          schools: this.universities.filter(u =>
            u.location[0] > 116 && u.location[0] < 117 &&
            u.location[1] > 39.5 && u.location[1] < 40.5
          )
        },
        {
          name: '上海地区',
          center: [121.48, 31.25],
          radius: 100, // 中等大小的气泡
          direction: 'right', // 向右侧引出
          schools: this.universities.filter(u =>
            u.location[0] > 121 && u.location[0] < 122 &&
            u.location[1] > 31 && u.location[1] < 32
          )
        },
        {
          name: '广州地区',
          center: [113.35, 23.13],
          radius: 90, // 减小气泡大小
          direction: 'topRight', // 向右上方引出，减少距离
          schools: this.universities.filter(u =>
            u.location[0] > 113 && u.location[0] < 114 &&
            u.location[1] > 23 && u.location[1] < 24
          )
        }
      ]

      // 为气泡区域内的学校计算新的位置
      bubbleRegions.forEach(region => {
        // 根据学校数量计算分布角度
        const schoolCount = region.schools.length
        region.schools.forEach((school, index) => {
          // 计算角度和距离，使学校均匀分布在圆形区域内
          const angle = (index / schoolCount) * Math.PI * 2
          const distance = region.radius * 0.6 // 距离中心的半径

          // 计算新的相对坐标
          school.relativePos = {
            x: Math.cos(angle) * distance,
            y: Math.sin(angle) * distance
          }
        })
      })


      // 创建学校与教授的映射关系
      const schoolProfessorsMap = new Map()
      this.universities.forEach(uni => {
        schoolProfessorsMap.set(uni.name, [])
      })

      this.professors.forEach(professor => {
        professor.universities.forEach(uni => {
          const professors = schoolProfessorsMap.get(uni.name) || []
          professors.push({
            name: professor.name,
            tenure: uni.tenure
          })
          schoolProfessorsMap.set(uni.name, professors)
        })
      })

      // 筛选出在两个或以上学校任教的教授
      const multiSchoolProfessors = this.professors.filter(p => p.universities.length >= 2)

      // 生成教授轨迹连线数据，使用原始坐标
      const generateProfessorLines = (professor) => {
        const lines = [];
        for (let i = 0; i < professor.universities.length - 1; i++) {
          const fromUni = professor.universities[i];
          const toUni = professor.universities[i + 1];

          lines.push({
            name: professor.name,
            fromUni: fromUni,
            toUni: toUni,
            coords: [fromUni.location, toUni.location]
          });
        }
        return lines;
      };

      const option = {
        backgroundColor: '#f5f5f5',

        tooltip: {
          trigger: 'item',
          formatter: (params) => {

            if (!(params.data != null)) {
              return params.name || '';
            }
            console.log('params', params)
            // 处理连线数据
            if (params.componentSubType === 'lines') {
              const lineData = params.data
              if (lineData && lineData.fromUni && lineData.toUni) {
                return `${lineData.name}教授<br/>
                       ${lineData.fromUni.name} (${lineData.fromUni.tenure})<br/>
                       ↓<br/>
                       ${lineData.toUni.name} (${lineData.toUni.tenure})`
              }
            }

            // 处理气泡区域的自定义元素
            if (params.seriesName === "放大气泡") {
              const regionIndex = params.dataIndex;
              // console.log('dataIndex',params.dataIndex)
              if (regionIndex !== undefined && bubbleRegions[regionIndex]) {
                const region = bubbleRegions[regionIndex];
                let html = `<div style="font-weight:bold;margin-bottom:5px;">${region.name}</div>`;
                region.schools.forEach(school => {
                  html += `<div style="margin-top:5px;"><b>${school.name}</b>: 影响力 ${school.value}</div>`;
                });
                return html;
              }
              return params.name || '';
            }

            // 处理普通学校点
            if (params.seriesName === '高校分布') {
              const schoolName = params.data.name;

              let html = `<div style="font-weight:bold;margin-bottom:5px;">${schoolName}</div>`;

              // 根据表格数据显示人物与学校的关系
              const relationships = params.data.relationships || [];
              if (relationships.length > 0) {
                relationships.forEach(rel => {
                  html += `<div>${rel.person}${rel.relationship}(${rel.time})</div>`;
                });
              }

              return html;
            }


            return params.name || '';
          }
        },
        legend: {
          type: 'scroll',
          orient: 'vertical',
          right: 10,
          top: 60,
          bottom: 20,
          data: [
            {
              name: '高校分布',
              icon: 'circle'
            },
            {
              name: '放大气泡',
              icon: 'circle'
            }
          ].concat(
            multiSchoolProfessors.map(p => ({
              name: p.name,
              icon: 'rect'
            }))
          ),
          textStyle: {
            color: '#333'
          },
          selected: {
            '高校分布': true,
            '放大气泡': true,
            ...multiSchoolProfessors.reduce((acc, prof) => {
              acc[prof.name] = true;
              return acc;
            }, {})
          },
          formatter: function (name) {
            if (name === '高校分布' || name === '放大气泡') {
              return name;
            }
            return name;
          }
        },
        visualMap: {
          type: 'continuous',
          min: 60,
          max: 100,
          text: ['影响力高', '影响力低'],
          inRange: {
            color: ['#d94e5d', '#eac736', '#50a3ba'].reverse()
          },
          calculable: true,
          dimension: 2,
          orient: 'vertical',
          right: 30,
          top: 'center',
          textStyle: {
            color: '#333'
          },
          seriesIndex: 0
        },
        geo: {
          map: 'china',
          roam: true,
          scaleLimit: {
            min: 1,
            max: 10
          },
          center: [116.37, 32.52], // 设置中心点为华中大学的位置
          zoom: 3, // 调整缩放级别，根据需要进行调整
          itemStyle: {
            areaColor: '#ffffff',
            borderColor: '#ccc',
            borderWidth: 1
          },
          emphasis: {
            itemStyle: {
              areaColor: '#f5f5f5'
            }
          },
          silent: true
        },
        series: [
          {
            name: '高校分布',
            type: 'scatter',
            coordinateSystem: 'geo',
            data: this.universities.map(u => ({
              name: u.name,
              value: [...u.location, u.value],
              category: u.category,
              relationships: u.relationships || []
            })),
            symbolSize: (val) => val[2] / 6,
            itemStyle: {
              borderColor: '#fff',
              borderWidth: 1
            },
            label: {
              show: true,
              position: 'left',
              formatter: '{b}',
              fontSize: 12,
              backgroundColor: 'rgba(255,255,255,0.7)',
              padding: [3, 5],
              borderRadius: 3,
              distance: 5
            },
            emphasis: {
              label: {
                show: true,
                backgroundColor: 'rgba(255,255,255,0.9)',
                borderColor: '#555',
                borderWidth: 1
              },
              itemStyle: {
                shadowBlur: 10,
                shadowColor: 'rgba(0,0,0,0.3)'
              }
            },
            zlevel: 1
          },
          {
            name: '放大气泡',
            type: 'custom',
            coordinateSystem: 'geo',
            renderItem: (params, api) => {
              const region = bubbleRegions[params.dataIndex]

              const coord = api.coord(region.center)
              const radius = region.radius

              // 计算引导线的位置
              let guideLineStart = [coord[0], coord[1]];
              let guideLineEnd = [...guideLineStart];
              let bubbleCenter = [...guideLineStart];

              // 根据方向设置引导线和气泡位置
              const offset = radius * 1.2; // 减小偏移距离
              switch (region.direction) {
                case 'rightBottom':
                  // 向右下方偏移
                  guideLineEnd[0] += offset;
                  bubbleCenter[0] = guideLineEnd[0] + radius * 0.3;
                  break;
                case 'right':
                  guideLineEnd[0] += offset;
                  bubbleCenter[0] = guideLineEnd[0] + radius * 0.3;
                  break;
                case 'topRight':
                  // 向右上方引出，减少距离
                  guideLineEnd[0] += offset * 0.5;
                  guideLineEnd[1] -= offset * 0.5;
                  bubbleCenter[0] = guideLineEnd[0] + radius * 0.2;
                  bubbleCenter[1] = guideLineEnd[1] - radius * 0.2;
                  break;
              }

              return {
                type: 'group',
                children: [
                  // 引导线
                  {
                    type: 'line',
                    shape: {
                      x1: guideLineStart[0],
                      y1: guideLineStart[1],
                      x2: guideLineEnd[0],
                      y2: guideLineEnd[1]
                    },
                    style: {
                      stroke: '#333',
                      lineWidth: 2,
                      lineDash: [5, 5]
                    }
                  },
                  // 气泡边框
                  {
                    type: 'circle',
                    shape: {
                      cx: bubbleCenter[0],
                      cy: bubbleCenter[1],
                      r: radius
                    },
                    style: {
                      fill: 'rgba(255, 255, 255, 0.9)',
                      stroke: '#333',
                      lineWidth: 2,
                      shadowBlur: 15,
                      shadowColor: 'rgba(0,0,0,0.3)',
                      shadowOffsetX: 3,
                      shadowOffsetY: 3
                    }
                  },
                  // 气泡标题
                  {
                    type: 'text',
                    style: {
                      text: region.name,
                      x: bubbleCenter[0],
                      y: bubbleCenter[1] - radius - 20, // 将文本位置设置在气泡上方
                      textAlign: 'center',
                      textVerticalAlign: 'middle',
                      fontSize: 16,
                      fontWeight: 'bold',
                      fill: '#333'
                    }
                  },
                  // 气泡内的热力点
                  ...region.schools.map(school => {
                    // 使用预先计算的相对位置
                    const relX = bubbleCenter[0] + school.relativePos.x;
                    const relY = bubbleCenter[1] + school.relativePos.y;

                    // 使用直接的颜色映射，根据影响力值选择颜色
                    let pointColor;
                    if (school.value >= 90) {
                      pointColor = '#d94e5d'; // 红色 - 最高影响力
                    } else if (school.value >= 80) {
                      pointColor = '#e67c51'; // 橙红色
                    } else if (school.value >= 70) {
                      pointColor = '#eac736'; // 黄色
                    } else {
                      pointColor = '#50a3ba'; // 蓝色 - 最低影响力
                    }

                    return {
                      type: 'group',
                      children: [
                        // 热力点
                        {
                          type: 'circle',
                          shape: {
                            cx: relX,
                            cy: relY,
                            r: school.value / 6
                          },
                          style: {
                            fill: pointColor,
                            shadowBlur: 10,
                            shadowColor: 'rgba(0,0,0,0.3)'
                          }
                        },
                        // 学校名称
                        {
                          type: 'text',
                          style: {
                            text: school.name,
                            x: relX,
                            y: relY - school.value / 5 - 5,
                            textAlign: 'center',
                            textVerticalAlign: 'bottom',
                            fontSize: 12,
                            fontWeight: 'normal',
                            fill: '#333',
                            backgroundColor: 'rgba(255,255,255,0.8)',
                            padding: [3, 5],
                            borderRadius: 3
                          }
                        }
                      ]
                    }
                  })
                ]
              }
            },

            data: bubbleRegions.map((_, index) => index),
            zlevel: 2
          },
          // 为每个教授创建单独的线系列
          ...multiSchoolProfessors.map(professor => ({
            name: professor.name,
            type: 'lines',
            coordinateSystem: 'geo',
            data: generateProfessorLines(professor),
            effect: {
              show: true,
              period: 6,
              trailLength: 0.5,
              symbol: 'arrow',
              symbolSize: 6
            },
            lineStyle: {
              color: professor.color,
              opacity: 0.8,
              width: 2,
              curveness: 0.3
            },
            zlevel: 3
          }))
        ]
      }

      mapChart.setOption(option)

      window.addEventListener('resize', () => {
        mapChart.resize()
      })
    }
  }
}
</script>

<style scoped>
.university-map-container {
  padding: 10px;
  background: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
}
</style>