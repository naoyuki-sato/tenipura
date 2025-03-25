<script setup>
  import { ref, computed, onMounted, watch } from 'vue';

  const selectedMatch = ref(1);

  const max_court_num = ref(2);
  const court_num = ref(1);

  const max_member_num = ref(3);
  const member_num = ref(4);

  const max_game_num = ref(3);

  const random = ref('しない')

  watch(court_num, (newVal) => {
    console.log(court_num.value);
    if (court_num.value === 1) {
      max_member_num.value = 3;
      member_num.value = 4;
    } else {
      max_member_num.value = 7;
      member_num.value = 8;
    }
  });

  watch(member_num, (newVal) => {
    console.log(member_num.value);
    if (member_num.value === 4) {
      max_game_num.value = 3;
    } else {
      max_game_num.value = 8;
    }
  });

  const doubles_pair = ref(null);
  const doubles_pair_court1 = ref([
    [1, 2, 3, 4],
    [1, 3, 2, 4],
    [1, 4, 2, 3],
  ]);
  const doubles_pair_court2 = ref([]);


  watch([court_num, member_num, random], () => {
    console.log('--------------------------');

    selectedMatch.value = 1;
    doubles_pair_court1.value.length = 0;
    doubles_pair_court2.value.length = 0;

    doubles_pair.value = get_doubles_data(court_num, member_num);
    if (random.value == 'する') {
      shuffle_doubles_data(court_num.value, member_num.value, doubles_pair.value);
    }
    
    if (court_num.value > 1) {
      for (let i = 0; i < doubles_pair.value.length; i++) {
        doubles_pair_court1.value.push(doubles_pair.value[i][0]);
        doubles_pair_court2.value.push(doubles_pair.value[i][1]);
      }
    } else {
      doubles_pair_court1.value = doubles_pair.value;
    }
  });

  function shuffle_array(array) {
  for (let i = array.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [array[i], array[j]] = [array[j], array[i]];
  }
  return array;
}

  function shuffle_doubles_data(court_num, member_num, doubles_pair) {
    var member_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12];
    member_list = member_list.slice(0, member_num);
    var shuffle_list = shuffle_array(member_list);
    console.log('court_num: ', court_num);
    console.log('member_num: ', member_num);
    console.log('doubles_pair: ', doubles_pair);
    console.log('member_list: ', member_list);
    console.log('shuffle_list: ', shuffle_list);

    if (court_num > 1) {
      for (let i = 0; i < doubles_pair.length; i++) {
        for (let j = 0; j < doubles_pair[i].length; j++) {
          for (let k = 0; k < doubles_pair[i][j].length; k++) {
            doubles_pair[i][j][k] = shuffle_list[doubles_pair[i][j][k] - 1];
          }
        }
      }
    } else {
      for (let i = 0; i < doubles_pair.length; i++) {
        for (let j = 0; j < doubles_pair[i].length; j++) {
          doubles_pair[i][j] = shuffle_list[doubles_pair[i][j] - 1];
        }
      }
    }
    console.log('doubles_pair: ', doubles_pair);
  }

  function get_doubles_data(court_num, member_num) {
    console.log(court_num.value);
    console.log(member_num.value);
    let doubles_pair = null;
    if (court_num.value === 1) {
      if (member_num.value === 4) {
        doubles_pair = [
          [1, 2, 3, 4],
          [1, 3, 2, 4],
          [1, 4, 2, 3],
        ];
      } else if (member_num.value === 5) {
        doubles_pair = [
          [1, 2, 3, 4],
          [1, 5, 2, 3],
          [1, 4, 2, 5],
          [1, 3, 4, 5],
          [2, 4, 3, 5],
          [1, 3, 2, 4],
          [3, 5, 1, 2],
          [4, 5, 1, 2],
          [3, 4, 1, 5],
          [2, 3, 4, 5],
          [1, 4, 2, 3],
          [2, 5, 1, 3],
          [2, 4, 1, 5],
          [3, 5, 1, 4],
          [2, 5, 3, 4],
        ];
      } else if (member_num.value === 6) {
        doubles_pair = [
          [1, 2, 3, 4],
          [5, 6, 1, 3],
          [2, 5, 4, 6],
          [1, 6, 2, 3],
          [2, 4, 1, 5],
          [3, 6, 4, 5],
          [1, 4, 2, 6],
          [3, 5, 1, 2],
          [3, 4, 5, 6],
          [1, 3, 2, 5],
          [2, 4, 1, 6],
          [3, 5, 4, 6],
          [1, 5, 2, 6],
          [2, 3, 4, 5],
          [1, 4, 3, 6],
        ];
      } else if (member_num.value === 7) {
        doubles_pair = [
          [1, 2, 3, 4],
          [5, 6, 1, 7],
          [2, 3, 5, 7],
          [1, 4, 2, 6],
          [3, 7, 4, 6],
          [2, 5, 1, 3],
          [4, 5, 6, 7],
          [1, 6, 2, 7],
          [3, 5, 2, 4],
          [1, 5, 3, 6],
          [4, 7, 1, 2],
          [3, 5, 4, 6],
          [2, 7, 3, 6],
          [1, 4, 5, 7],
          [2, 6, 4, 5],
        ];
      } else if (member_num.value === 8) {
        doubles_pair = [
          [1, 2, 3, 4],
          [5, 6, 7, 8],
          [1, 3, 5, 7],
          [2, 4, 6, 8],
          [1, 5, 4, 8],
          [2, 3, 6, 7],
          [1, 6, 4, 7],
          [2, 5, 3, 8],
          [1, 7, 2, 8],
          [3, 5, 4, 6],
          [1, 8, 3, 6],
          [2, 7, 4, 5],
          [1, 4, 3, 7],
          [2, 6, 5, 8],
          [1, 2, 5, 6],
        ];
      }
    } else {
      if (member_num.value === 8) {
        doubles_pair = [
          [
            [1, 2, 3, 4],
            [5, 6, 7, 8],
          ],
          [
            [1, 3, 5, 7],
            [2, 4, 6, 8],
          ],
          [
            [1, 4, 5, 8],
            [2, 3, 6, 7],
          ],
          [
            [1, 5, 2, 6],
            [3, 7, 4, 8],
          ],
          [
            [1, 7, 2, 8],
            [3, 5, 4, 6],
          ],
          [
            [1, 6, 3, 8],
            [2, 5, 4, 7],
          ],
          [
            [1, 8, 2, 7],
            [3, 6, 4, 5],
          ],
          [
            [1, 4, 6, 7],
            [2, 3, 5, 8],
          ],
          [
            [1, 2, 5, 6],
            [3, 4, 7, 8],
          ],
          [
            [1, 5, 3, 7],
            [2, 6, 4, 8],
          ],
        ];
      } else if (member_num.value === 9) {
        doubles_pair = [
          [
            [1, 2, 3, 4],
            [5, 6, 7, 8],
          ],
          [
            [1, 9, 3, 5],
            [2, 4, 6, 7],
          ],
          [
            [1, 8, 4, 5],
            [2, 9, 3, 6],
          ],
          [
            [1, 7, 2, 5],
            [8, 9, 4, 6],
          ],
          [
            [3, 8, 1, 6],
            [4, 7, 5, 9],
          ],
          [
            [2, 8, 3, 7],
            [6, 9, 1, 4],
          ],
          [
            [2, 6, 5, 8],
            [1, 3, 7, 9],
          ],
          [
            [2, 7, 1, 5],
            [3, 9, 4, 8],
          ],
          [
            [2, 3, 4, 9],
            [5, 7, 6, 8],
          ],
          [
            [1, 2, 7, 8],
            [3, 4, 5, 6],
          ],
        ];
      } else if (member_num.value === 10) {
        doubles_pair = [
          [
            [1, 2, 3, 4],
            [5, 6, 7, 8],
          ],
          [
            [1, 9, 3, 5],
            [2, 10, 4, 6],
          ],
          [
            [7, 9, 2, 5],
            [8, 10, 1, 6],
          ],
          [
            [3, 7, 1, 10],
            [4, 8, 2, 9],
          ],
          [
            [3, 6, 8, 9],
            [4, 5, 7, 10],
          ],
          [
            [1, 4, 5, 8],
            [2, 3, 6, 7],
          ],
          [
            [3, 9, 4, 10],
            [1, 7, 2, 8],
          ],
          [
            [5, 10, 1, 3],
            [6, 9, 2, 4],
          ],
          [
            [5, 7, 2, 6],
            [1, 8, 9, 10],
          ],
          [
            [3, 8, 4, 7],
            [5, 9, 6, 10],
          ],
        ];
      } else if (member_num.value === 11) {
        doubles_pair = [
          [
            [1, 2, 3, 4],
            [5, 6, 7, 8],
          ],
          [
            [9, 10, 1, 5],
            [2, 11, 3, 6],
          ],
          [
            [4, 7, 9, 11],
            [8, 10, 1, 6],
          ],
          [
            [2, 4, 8, 9],
            [3, 5, 7, 10],
          ],
          [
            [1, 11, 3, 8],
            [2, 6, 7, 9],
          ],
          [
            [4, 5, 6, 10],
            [7, 11, 1, 8],
          ],
          [
            [2, 5, 10, 11],
            [3, 9, 1, 4],
          ],
          [
            [6, 8, 4, 11],
            [2, 7, 3, 10],
          ],
          [
            [1, 3, 6, 7],
            [5, 9, 2, 8],
          ],
          [
            [4, 10, 6, 9],
            [5, 8, 3, 11],
          ],
        ];
      } else if (member_num.value === 12) {
        doubles_pair = [
          [
            [1, 2, 3, 4],
            [5, 6, 7, 8],
          ],
          [
            [9, 10, 1, 5],
            [11, 12, 2, 6],
          ],
          [
            [3, 7, 9, 11],
            [4, 8, 10, 12],
          ],
          [
            [1, 6, 3, 8],
            [2, 5, 4, 7],
          ],
          [
            [2, 9, 6, 10],
            [1, 11, 5, 12],
          ],
          [
            [3, 9, 7, 12],
            [4, 10, 8, 11],
          ],
          [
            [1, 7, 2, 8],
            [3, 5, 4, 6],
          ],
          [
            [1, 9, 6, 12],
            [2, 10, 5, 11],
          ],
          [
            [3, 10, 7, 11],
            [4, 9, 8, 12],
          ],
          [
            [1, 4, 6, 7],
            [2, 3, 5, 8],
          ],
        ];
      }
    }
    return doubles_pair;
  }
</script>

<template>
  <v-app>
    <v-main>
      <v-container>
        <h3><strong>ダブルス 組み合わせ表</strong></h3>
        <p>
          コート数、参加人数を選んで下さい。<br />ダブルスの組み合わせが表示されます。
        </p>
        <br />
        <p><strong>コート数</strong></p>
        <v-radio-group v-model="court_num" inline>
          <v-radio
            v-for="n in max_court_num"
            :key="n"
            :label="n + 'コート'"
            :value="n"
            color="primary"
          ></v-radio>
        </v-radio-group>

        <p><strong>参加人数</strong></p>
        <v-radio-group v-model="member_num" inline>
          <v-radio
            v-for="n in 5"
            :key="n"
            :label="n + max_member_num + '名'"
            :value="n + max_member_num"
            color="primary"
          ></v-radio>
        </v-radio-group>
    
        <p><strong>順番をランダム</strong></p>
            <v-switch
    v-model="random"
    :label="`${random}`"
    false-value="しない"
    true-value="する"
    color="primary"
    hide-details
  ></v-switch>
  <br/>
        

        <p><strong>試合順</strong></p>
        <v-table v-if="doubles_pair_court1 !== null">
          <thead>
            <tr>
              <th><strong>番号</strong></th>
              <th><strong>ペア1</strong></th>
              <th></th>
              <th><strong>ペア2</strong></th>
            </tr>
          </thead>
          <tbody>
            <template v-for="n in max_game_num" :key="n">
              <tr>
                <td :rowspan="court_num">
                  <v-radio-group v-model="selectedMatch" :value="n">
                    <v-radio :value="n" :label="`${n}`"></v-radio>
                  </v-radio-group>
                </td>
                <td class="large-text">
                  {{ doubles_pair_court1[n - 1][0] }},
                  {{ doubles_pair_court1[n - 1][1] }}
                </td>
                <td>vs</td>
                <td class="large-text">
                  {{ doubles_pair_court1[n - 1][2] }},
                  {{ doubles_pair_court1[n - 1][3] }}
                </td>
              </tr class="large-text">
              <tr v-if="court_num > 1">
                <td class="large-text">
                  {{ doubles_pair_court2[n - 1][0] }},
                  {{ doubles_pair_court2[n - 1][1] }}
                </td>
                <td>vs</td>
                <td class="large-text">
                  {{ doubles_pair_court2[n - 1][2] }},
                  {{ doubles_pair_court2[n - 1][3] }}
                </td>
              </tr>
            </template>
          </tbody>
        </v-table>
      </v-container>
    </v-main>
  </v-app>
</template>

<style>
  .large-text {
    font-size: 1.3em;
  }
</style>
