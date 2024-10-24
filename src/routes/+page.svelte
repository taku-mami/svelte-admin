<script>
    import { onMount } from 'svelte';

    // Table data
    let rows = [
        { 품목: "아사이 소르베", 품명: "아사이 소르베", 규격: "7kg/bucket", 재고단위: "BUCKET", 발주단위: "1 BUCKET (7kg)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 파소카	PB 크럼브	1kg/pack	PACK	1 BOX (1kg , 4팩)
        { 품목: "파소카", 품명: "PB 크럼브", 규격: "1kg/pack", 재고단위: "PACK", 발주단위: "1 BOX (1kg , 4팩)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // RTD 캔음료	마차 에너지 티	1ea/can	CAN	1 BOX (24ea)
        { 품목: "RTD 캔음료", 품명: "마차 에너지 티", 규격: "1ea/can", 재고단위: "CAN", 발주단위: "1 BOX (24ea)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 팩오크	팩오크	24ea/box	EA	1 BOX (96ea, 4팩)
        { 품목: "팩오크", 품명: "팩오크", 규격: "24ea/box", 재고단위: "EA", 발주단위: "1 BOX (96ea, 4팩)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 그래놀라	샘트리 그래놀라	10kg/box	10kg	1 BOX (10kg , 1팩)
        { 품목: "그래놀라", 품명: "샘트리 그래놀라", 규격: "10kg/box", 재고단위: "10kg", 발주단위: "1 BOX (10kg , 1팩)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 크러쉬드 피넛	샘트리 크러쉬드 피넛	10kg*2/box	10kg	1 BOX (10kg , 2팩)
        { 품목: "크러쉬드 피넛", 품명: "샘트리 크러쉬드 피넛", 규격: "10kg*2/box", 재고단위: "10kg", 발주단위: "1 BOX (10kg , 2팩)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 크러쉬드 아몬드	샘트리 크러쉬드 아몬드	1kg/pack	1kg	1팩 (1kg ,  1팩)
        { 품목: "크러쉬드 아몬드", 품명: "샘트리 크러쉬드 아몬드", 규격: "1kg/pack", 재고단위: "1kg", 발주단위: "1팩 (1kg ,  1팩)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 캐슈넛	샘트리 볶은 캐슈넛	1kg/pack	1kg	1팩 (1kg ,  1팩)
        { 품목: "캐슈넛", 품명: "샘트리 볶은 캐슈넛", 규격: "1kg/pack", 재고단위: "1kg", 발주단위: "1팩 (1kg ,  1팩)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 치아시드	건강중심 치아시드	1kg/pack	1kg	1팩 (1kg , 1팩)
        { 품목: "치아시드", 품명: "건강중심 치아시드", 규격: "1kg/pack", 재고단위: "1kg", 발주단위: "1팩 (1kg , 1팩)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 해바라기 씨앗	샘트리 해바라기 씨앗	1kg/pack	1kg	1팩 (1kg ,  1팩)
        { 품목: "해바라기 씨앗", 품명: "샘트리 해바라기 씨앗", 규격: "1kg/pack", 재고단위: "1kg", 발주단위: "1팩 (1kg ,  1팩)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 코코넛 슬라이스	썸앤썸 코코넛 슬라이스	1kg/pack	1kg	1 BOX (1kg , 15팩)
        { 품목: "코코넛 슬라이스", 품명: "썸앤썸 코코넛 슬라이스", 규격: "1kg/pack", 재고단위: "1kg", 발주단위: "1 BOX (1kg , 15팩)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 푸드팜 카카오닙스	카카오닙스	1kg/pack	1kg	1팩 (1kg ,  1팩)
        { 품목: "푸드팜 카카오닙스", 품명: "카카오닙스", 규격: "1kg/pack", 재고단위: "1kg", 발주단위: "1팩 (1kg ,  1팩)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 코코넛 밀크	허니트리 리치 코코넛 밀크	1L/pack	1L	BOX (12L , 12팩)
        { 품목: "코코넛 밀크", 품명: "허니트리 리치 코코넛 밀크", 규격: "1L/pack", 재고단위: "1L", 발주단위: "BOX (12L , 12팩)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 구기자	"남양구기자영농조합 청양 건구기자"	500g/pack	500g	1 낱개 (500g)
        { 품목: "구기자", 품명: "남양구기자영농조합 청양 건구기자", 규격: "500g/pack", 재고단위: "500g", 발주단위: "1 낱개 (500g)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 냉동 망고 퓨레	골든킹 프리미엄 망고 퓨레	1kg/pack	1kg	1 BOX (1kg , 6팩)
        { 품목: "냉동 망고 퓨레", 품명: "골든킹 프리미엄 망고 퓨레", 규격: "1kg/pack", 재고단위: "1kg", 발주단위: "1 BOX (1kg , 6팩)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 냉동 패션후르츠 퓨레	신정푸드 패션후르츠 퓨레	1kg/pack	1kg	1 BOX (1kg , 6팩)
        { 품목: "냉동 패션후르츠 퓨레", 품명: "신정푸드 패션후르츠 퓨레", 규격: "1kg/pack", 재고단위: "1kg", 발주단위: "1 BOX (1kg , 6팩)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 요거트	서울우유 더 진한 플레인 요거트	2.45L/pack	2.45L	1 낱개 (2.45L)
        { 품목: "요거트", 품명: "서울우유 더 진한 플레인 요거트", 규격: "2.45L/pack", 재고단위: "2.45L", 발주단위: "1 낱개 (2.45L)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 전지분유	서울우유 전지분유	1kg/pack	1kg	1 낱개 (1kg)
        { 품목: "전지분유", 품명: "서울우유 전지분유", 규격: "1kg/pack", 재고단위: "1kg", 발주단위: "1 낱개 (1kg)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 동물성 단백질	NS포대유청 단백질 바닐라	2kg/pack	PACK	1 낱개 (2kg)
        { 품목: "동물성 단백질", 품명: "NS포대유청 단백질 바닐라", 규격: "2kg/pack", 재고단위: "PACK", 발주단위: "1 낱개 (2kg)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 비건 단백질	"올게인 오가닉 식물성 단백질 바닐라"	920g/pack	PACK	1 낱개 (920g)
        { 품목: "비건 단백질", 품명: "올게인 오가닉 식물성 단백질 바닐라", 규격: "920g/pack", 재고단위: "PACK", 발주단위: "1 낱개 (920g)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 피넛버터	썸앤썸 땅콩버터	2kg/pack	2kg	1 BOX (2kg , 5팩)
        { 품목: "피넛버터", 품명: "썸앤썸 땅콩버터", 규격: "2kg/pack", 재고단위: "2kg", 발주단위: "1 BOX (2kg , 5팩)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 꿀	더비 사양벌꿀	2kg/pack	2kg	1 낱개 (2kg)
        { 품목: "꿀", 품명: "더비 사양벌꿀", 규격: "2kg/pack", 재고단위: "2kg", 발주단위: "1 낱개 (2kg)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 바나나	델몬트/돌 바나나	14kg/box	14kg BOX	BOX (14kg)
        { 품목: "바나나", 품명: "델몬트/돌 바나나", 규격: "14kg/box", 재고단위: "14kg BOX", 발주단위: "BOX (14kg)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 딸기	딸기 중과	2kg/pack	2kg PACK	1팩 (2kg)
        { 품목: "딸기", 품명: "딸기 중과", 규격: "2kg/pack", 재고단위: "2kg PACK", 발주단위: "1팩 (2kg)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 블루베리	블루베리 국내산/칠레산	100g*10/box	1kg BOX	BOX (1kg , 10팩)
        { 품목: "블루베리", 품명: "블루베리 국내산/칠레산", 규격: "100g*10/box", 재고단위: "1kg BOX", 발주단위: "BOX (1kg , 10팩)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 },
        // 키위	키위	500g/box	0.5kg BOX	BOX (0.5kg)
        { 품목: "키위", 품명: "키위", 규격: "500g/box", 재고단위: "0.5kg BOX", 발주단위: "BOX (0.5kg)", 전일재고: 0, 발주: 0, 입고: 0, 재고: 0, 사용량: 0 }
    ]

    let keys = Object.keys(rows[0])

    // Save the updated rows to localStorage
    function saveToLocalStorage() {
        localStorage.setItem("tableData", JSON.stringify(rows));
    }

    // Load data from localStorage when the component is mounted
    onMount(() => {
        const savedData = localStorage.getItem('tableData');
        if (savedData) {
        rows = JSON.parse(savedData);
        }
    });

</script>

<style>
    /* Add some custom CSS if needed */
    td[contenteditable] {
      /* border: 1px solid transparent;
      padding: 0.5rem; */
    }
    
    td[contenteditable]:focus {
      outline: 1px solid blue;
    }
</style>

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Editable Table with Tailwind CSS</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 p-10">
  <div class="container mx-auto">
    <h1 class="text-2xl font-bold mb-5">원료 재고 관리 시트</h1>
    <table class="min-w-full bg-white border border-gray-300 rounded-lg">
      <thead>
        <tr class="bg-gray-100 border-b border-gray-300">
          {#each keys as key}
            <th class="py-3 px-5 text-left">{key}</th>
          {/each}
        </tr>
      </thead>
      <tbody>
        {#each rows as row, index}
            <tr class="border-b border-gray-300">
            <td class="py-3 px-5">{row.품목}</td>
            <td class="py-3 px-5">{row.품명}</td>
            <td class="py-3 px-5">{row.규격}</td>
            <td class="py-3 px-5">{row.재고단위}</td>
            <td class="py-3 px-5">{row.발주단위}</td>
            <!-- Make the Occupation column editable -->
            <td
                class="py-3 px-5"
                contenteditable="true"
                on:input={event => {rows[index].전일재고 = event.target.innerText; saveToLocalStorage(); }}
            >{row.전일재고}</td>
            <td
                class="py-3 px-5"
                contenteditable="true"
                on:input={event => {rows[index].발주 = event.target.innerText; saveToLocalStorage(); }}
            >{row.발주}</td>
            <td
                class="py-3 px-5"
                contenteditable="true"
                on:input={event => {rows[index].입고 = event.target.innerText; saveToLocalStorage(); }}
            >{row.입고}</td>
            <td
                class="py-3 px-5"
                contenteditable="true"
                on:input={event => {rows[index].재고 = event.target.innerText; saveToLocalStorage(); }}
            >{row.재고}</td>
            <td
                class="py-3 px-5"
                contenteditable="true"
                on:input={event => {rows[index].사용량 = event.target.innerText; saveToLocalStorage(); }}
            >{row.사용량}</td>
            </tr>
        {/each}
      </tbody>
    </table>
  </div>
</body>
