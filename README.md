<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>스마트 정압기 매뉴얼</title>
    <!-- Tailwind CSS 연동 -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Lucide 아이콘 연동 -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        /* 기본 애니메이션 및 스타일 */
        body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; -webkit-tap-highlight-color: transparent; }
        .fade-in { animation: fadeIn 0.3s ease-in-out; }
        .slide-up { animation: slideUp 0.3s ease-out; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        @keyframes slideUp { from { transform: translateY(20px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
        .view-section { display: none; }
        .view-section.active { display: block; }
        
        /* 커스텀 스크롤바 (팝업용) */
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: #f1f5f9; border-radius: 4px; }
        ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #94a3b8; }
        
        /* Details 애니메이션 처리를 위한 간단한 핵 */
        details > summary { list-style: none; }
        details > summary::-webkit-details-marker { display: none; }
        details[open] summary ~ * { animation: fadeIn 0.3s ease-in-out; }
    </style>
</head>
<body class="bg-gray-50 min-h-screen">
    <div class="max-w-md mx-auto bg-gray-50 min-h-screen shadow-2xl relative overflow-hidden flex flex-col">
        
        <!-- 글로벌 헤더 -->
        <header class="bg-white border-b border-gray-200 sticky top-0 z-10">
            <div class="flex items-center justify-between p-4">
                <div class="flex items-center gap-3">
                    <button id="btn-back" class="hidden p-1 -ml-2 rounded-lg hover:bg-gray-100 active:bg-gray-200" onclick="changeView('home')">
                        <i data-lucide="chevron-left" class="w-7 h-7 text-gray-700"></i>
                    </button>
                    <h1 class="text-lg font-extrabold text-gray-900 tracking-tight">스마트 정압기 매뉴얼</h1>
                </div>
                <div class="w-8 h-8 bg-blue-600 rounded-lg flex items-center justify-center shadow-sm">
                    <span class="text-white font-black text-xs">GAS</span>
                </div>
            </div>
        </header>

        <!-- 메인 컨텐츠 영역 -->
        <main class="pb-8 flex-1">
            
            <!-- 1. 홈 화면 (home) -->
            <section id="view-home" class="view-section active p-4 space-y-6 fade-in">
                <!-- 장비 요약 정보 카드 -->
                <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-5 relative overflow-hidden">
                    <div class="absolute top-0 right-0 w-20 h-20 bg-blue-50 rounded-bl-full -z-0"></div>
                    <div class="flex justify-between items-start mb-4 relative z-10">
                        <div>
                            <h2 class="text-xl font-bold text-gray-800">개정통사 정압기</h2>
                            <p class="text-sm text-gray-500 font-mono mt-1">ID: GS-REG-2026-01</p>
                        </div>
                        <span class="inline-flex items-center gap-1 px-2.5 py-1 rounded-full text-xs font-medium bg-green-100 text-green-800 border border-green-200">
                            <span class="w-2 h-2 rounded-full bg-green-500 animate-pulse"></span>
                            정상 가동중
                        </span>
                    </div>
                    <div class="grid grid-cols-2 gap-y-2 text-sm text-gray-600 relative z-10">
                        <p><span class="text-gray-400">타입:</span> 1098EGR,바스파워텍</p>
                        <p><span class="text-gray-400">설치일:</span> 2025.06.23</p>
                        <div class="col-span-2 flex items-center justify-between pt-3 mt-1 border-t border-gray-100">
                            <p><span class="text-gray-400">최근 점검일:</span> 2026-04-28</p>
                            <button onclick="openInfoPopup()" class="flex items-center gap-1.5 bg-blue-50 text-blue-700 px-3 py-1.5 rounded-lg text-xs font-bold border border-blue-100 hover:bg-blue-100 active:bg-blue-200 transition-colors shadow-sm">
                                <i data-lucide="info" class="w-3.5 h-3.5"></i> 정압기 정보 보기
                            </button>
                        </div>
                    </div>
                </div>

                <!-- 메인 메뉴 그리드 -->
                <div class="grid grid-cols-2 gap-4">
                    <button onclick="changeView('emergency')" class="flex flex-col items-center justify-center p-5 bg-red-50 rounded-xl border border-red-100 shadow-sm active:bg-red-100 transition-colors group">
                        <div class="w-12 h-12 bg-red-500 rounded-full flex items-center justify-center mb-3 shadow-md group-active:scale-95 transition-transform">
                            <i data-lucide="alert-triangle" class="text-white w-6 h-6"></i>
                        </div>
                        <span class="font-bold text-red-700 text-sm">긴급 조치 가이드</span>
                    </button>
                    <button onclick="changeView('manual')" class="flex flex-col items-center justify-center p-5 bg-blue-50 rounded-xl border border-blue-100 shadow-sm active:bg-blue-100 transition-colors group">
                        <div class="w-12 h-12 bg-blue-500 rounded-full flex items-center justify-center mb-3 shadow-md group-active:scale-95 transition-transform">
                            <i data-lucide="book-open" class="text-white w-6 h-6"></i>
                        </div>
                        <span class="font-bold text-blue-800 text-sm">표준 운영 절차</span>
                    </button>
                    <button onclick="changeView('manualLinks')" class="flex flex-col items-center justify-center p-5 bg-purple-50 rounded-xl border border-purple-100 shadow-sm active:bg-purple-100 transition-colors group">
                        <div class="w-12 h-12 bg-purple-500 rounded-full flex items-center justify-center mb-3 shadow-md group-active:scale-95 transition-transform">
                            <i data-lucide="folder-open" class="text-white w-6 h-6"></i>
                        </div>
                        <span class="font-bold text-purple-800 text-sm">매뉴얼 및 도면</span>
                    </button>
                    <button onclick="changeView('ssvReset')" class="flex flex-col items-center justify-center p-5 bg-green-50 rounded-xl border border-green-100 shadow-sm active:bg-green-100 transition-colors group">
                        <div class="w-12 h-12 bg-green-500 rounded-full flex items-center justify-center mb-3 shadow-md group-active:scale-95 transition-transform">
                            <i data-lucide="refresh-cw" class="text-white w-6 h-6"></i>
                        </div>
                        <span class="font-bold text-green-800 text-sm">SSV 복귀 방법</span>
                    </button>
                    <button onclick="changeView('checklist')" class="flex flex-col items-center justify-center p-5 bg-teal-50 rounded-xl border border-teal-100 shadow-sm active:bg-teal-100 transition-colors group">
                        <div class="w-12 h-12 bg-teal-500 rounded-full flex items-center justify-center mb-3 shadow-md group-active:scale-95 transition-transform">
                            <i data-lucide="shield-check" class="text-white w-6 h-6"></i>
                        </div>
                        <span class="font-bold text-teal-800 text-sm">일일 안전 점검</span>
                    </button>
                    <button onclick="changeView('contact')" class="flex flex-col items-center justify-center p-5 bg-gray-50 rounded-xl border border-gray-200 shadow-sm active:bg-gray-100 transition-colors group">
                        <div class="w-12 h-12 bg-gray-600 rounded-full flex items-center justify-center mb-3 shadow-md group-active:scale-95 transition-transform">
                            <i data-lucide="phone-call" class="text-white w-6 h-6"></i>
                        </div>
                        <span class="font-bold text-gray-800 text-sm">비상 연락망</span>
                    </button>
                </div>
            </section>

            <!-- 2. 긴급 조치 가이드 뷰 (emergency) -->
            <section id="view-emergency" class="view-section p-4 space-y-4 slide-up">
                <div class="bg-red-600 text-white p-4 rounded-xl shadow-md flex items-center gap-3">
                    <i data-lucide="alert-triangle" class="w-8 h-8"></i>
                    <div>
                        <h2 class="text-xl font-bold">가스 누출 및 긴급 상황</h2>
                        <p class="text-red-100 text-sm">즉각적인 조치가 필요합니다</p>
                    </div>
                </div>
                <div class="bg-white rounded-xl shadow-sm border border-gray-200 overflow-hidden">
                    <div class="p-4 border-b border-gray-100 bg-gray-50 font-bold text-gray-800">초동 조치 단계</div>
                    <div class="p-4 space-y-4">
                        <div class="flex gap-4 items-start">
                            <div class="bg-red-100 text-red-600 font-bold w-8 h-8 rounded-full flex items-center justify-center flex-shrink-0">1</div>
                            <div>
                                <h3 class="font-bold text-gray-800">주위 화기 통제 및 환기</h3>
                                <p class="text-sm text-gray-600 mt-1">인근의 모든 화기를 즉시 차단하고, 스파크가 발생할 수 있는 전자기기 사용을 금지합니다. 실내 정압기실의 경우 방폭 환풍기를 최대 출력으로 가동하십시오.</p>
                            </div>
                        </div>
                        <div class="flex gap-4 items-start">
                            <div class="bg-red-100 text-red-600 font-bold w-8 h-8 rounded-full flex items-center justify-center flex-shrink-0">2</div>
                            <div>
                                <h3 class="font-bold text-gray-800">전단/후단 차단 밸브(MOV) 폐쇄</h3>
                                <p class="text-sm text-gray-600 mt-1">압력계가 비정상적으로 상승하거나 누출음이 들릴 경우, 정압기 입구측 메인 밸브(V-101)를 최우선으로 차단하십시오.</p>
                            </div>
                        </div>
                        <div class="flex gap-4 items-start">
                            <div class="bg-red-100 text-red-600 font-bold w-8 h-8 rounded-full flex items-center justify-center flex-shrink-0">3</div>
                            <div>
                                <h3 class="font-bold text-gray-800">중앙 통제실 즉시 보고</h3>
                                <p class="text-sm text-gray-600 mt-1">상황 발생 즉시 통제실(063-440-7788)로 현장 상황(누출 압력, 냄새 유무, 주변 통제 상황)을 보고하십시오.</p>
                            </div>
                        </div>
                        <div class="flex gap-4 items-start">
                            <div class="bg-red-100 text-red-600 font-bold w-8 h-8 rounded-full flex items-center justify-center flex-shrink-0">4</div>
                            <div>
                                <h3 class="font-bold text-gray-800">비상출동대기조 가동</h3>
                                <p class="text-sm text-gray-600 mt-1">주간에는 상황실 통제를 받아 조치하지만, 야간 또는 휴일 시 비상출동 대기자의 지원을 받으십시오.</p>
                            </div>
                        </div>
                        <div class="flex gap-4 items-start">
                            <div class="bg-red-100 text-red-600 font-bold w-8 h-8 rounded-full flex items-center justify-center flex-shrink-0">5</div>
                            <div>
                                <h3 class="font-bold text-gray-800">정압기 특이사항 문의처</h3>
                                <p class="text-sm text-gray-600 mt-1">공급관리팀 김진홍 대리 010-4567-6733.</p>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- 3. 표준 운영 절차 (manual) -->
            <section id="view-manual" class="view-section p-4 space-y-4 slide-up">
                <div class="bg-blue-600 text-white p-4 rounded-xl shadow-md flex items-center gap-3">
                    <i data-lucide="book-open" class="w-8 h-8"></i>
                    <div>
                        <h2 class="text-xl font-bold">표준 운영 매뉴얼</h2>
                        <p class="text-blue-100 text-sm">일반 가동, 정지 및 점검 절차</p>
                    </div>
                </div>
                <div class="space-y-3">
                    <!-- 제1장 -->
                    <details class="bg-white rounded-lg shadow-sm border border-gray-200 group">
                        <summary class="font-bold p-4 cursor-pointer flex justify-between items-center text-gray-800 select-none">
                            제1장. 정압기 기동(Start-up) 절차
                            <i data-lucide="chevron-down" class="text-blue-500 group-open:rotate-180 transition-transform w-5 h-5"></i>
                        </summary>
                        <div class="p-4 border-t border-gray-100 text-sm text-gray-600 space-y-2 bg-gray-50">
                            <p>1. 정압기 전후단 압력계 및 온도계의 영점을 확인한다.</p>
                            <p>2. 바이패스(Bypass) 밸브가 완전히 닫혀 있는지 확인한다.</p>
                            <p>3. 후단 배관의 퍼지(Purge)가 완료되었는지 확인한다.</p>
                            <p>4. 출구측 밸브(V-102)를 10% 개방한다.</p>
                            <p>5. 입구측 밸브(V-101)를 천천히 개방하며 조정기(Regulator)의 작동 압력을 확인한다.</p>
                            <p>6. 설정 압력(Target Pressure)에 도달하면 입/출구 밸브를 100% 개방한다.</p>
                        </div>
                    </details>
                    <!-- 제2장 -->
                    <details class="bg-white rounded-lg shadow-sm border border-gray-200 group">
                        <summary class="font-bold p-4 cursor-pointer flex justify-between items-center text-gray-800 select-none">
                            제2장. 정압기 정지(Shut-down) 절차
                            <i data-lucide="chevron-down" class="text-blue-500 group-open:rotate-180 transition-transform w-5 h-5"></i>
                        </summary>
                        <div class="p-4 border-t border-gray-100 text-sm text-gray-600 space-y-2 bg-gray-50">
                            <p>1. 2차측(출구) 메인 밸브(V-102)를 천천히 완전히 차단한다.</p>
                            <p>2. 1차측(입구) 메인 밸브(V-101)를 차단한다.</p>
                            <p>3. 정압기 내부 압력을 제거하기 위해 벤트(Vent) 밸브를 열어 잔류 가스를 안전한 곳으로 배출한다.</p>
                            <p>4. 전후단 압력계가 '0'을 지시하는지 반드시 확인한다.</p>
                            <p>5. 장기 정지 시, SSV(안전차단밸브)를 수동으로 차단 상태에 둔다.</p>
                        </div>
                    </details>
                    <!-- 제3장 -->
                    <details class="bg-white rounded-lg shadow-sm border border-gray-200 group">
                        <summary class="font-bold p-4 cursor-pointer flex justify-between items-center text-gray-800 select-none">
                            제3장. SSV(안전차단밸브) 복구 절차
                            <i data-lucide="chevron-down" class="text-blue-500 group-open:rotate-180 transition-transform w-5 h-5"></i>
                        </summary>
                        <div class="p-4 border-t border-gray-100 text-sm text-gray-600 space-y-2 bg-gray-50">
                            <p>1. SSV 작동 원인(과압 또는 저압)을 먼저 파악하고, 이상 요인을 완벽히 제거한다.</p>
                            <p>2. 정압기 전후단 메인 밸브가 차단되어 있는지 확인한다.</p>
                            <p>3. 복구용 렌치(또는 레버)를 조작하여 SSV 내부의 이퀄라이징 밸브를 먼저 개방해 전후단 압력을 평형 상태로 맞춘다.</p>
                            <p>4. 압력 평형이 이루어지면 레버를 끝까지 당겨 걸쇠(Latch)가 정상적으로 고정되도록 리셋한다.</p>
                            <p>5. '제1장 기동 절차'에 따라 밸브를 서서히 열어 재가동한다.</p>
                        </div>
                    </details>
                    <!-- 제4장 -->
                    <details class="bg-white rounded-lg shadow-sm border border-gray-200 group">
                        <summary class="font-bold p-4 cursor-pointer flex justify-between items-center text-gray-800 select-none">
                            제4장. 필터(Filter) 차압 점검
                            <i data-lucide="chevron-down" class="text-blue-500 group-open:rotate-180 transition-transform w-5 h-5"></i>
                        </summary>
                        <div class="p-4 border-t border-gray-100 text-sm text-gray-600 space-y-2 bg-gray-50">
                            <p>1. 차압계(DPG)의 지시치를 확인합니다.</p>
                            <p>2. 필터 차압계가 이동이 있을 시 원인을 파악 합니다.</p>
                            <p>3. 조금 이동한 정도가 아니라 지시계가 반대방향으로 이동한 경우 즉각적인 보고를 통해 분해정비를 실시합니다..</p>
                            <p>4. 필터 차압계가 동작했다는 것은 이물질이 발생했다는 것이므로 보고를 통한 점검이 필요합니다..</p>
                        </div>
                    </details>
                    <!-- 제5장 -->
                    <details class="bg-white rounded-lg shadow-sm border border-gray-200 group">
                        <summary class="font-bold p-4 cursor-pointer flex justify-between items-center text-gray-800 select-none">
                            제5장. 일상 순회 점검 주요 항목
                            <i data-lucide="chevron-down" class="text-blue-500 group-open:rotate-180 transition-transform w-5 h-5"></i>
                        </summary>
                        <div class="p-4 border-t border-gray-100 text-sm text-gray-600 space-y-2 bg-gray-50">
                            <p>1. <strong>누출 점검:</strong> 플랜지 연결부 및 밸브류에 비눗물 또는 휴대용 검지기를 사용하여 가스 누출 여부를 확인한다.</p>
                            <p>2. <strong>계기판 확인:</strong> 압력계, 온도계, 차압계가 정상 운전 범위를 지시하고 있는지 기록한다.</p>
                            <p>3. <strong>이상 징후:</strong> 가스 냄새, 배관의 이상 진동(헌팅 현상), 비정상적인 소음 발생 여부를 살핀다.</p>
                            <p>4. <strong>환경 점검:</strong> 정압기실 내부 환기구 막힘 여부 및 배수설비 및 부식 여부를 확인한다.</p>
                        </div>
                    </details>
                </div>
            </section>

            <!-- 4. 매뉴얼 및 도면 (manualLinks) -->
            <section id="view-manualLinks" class="view-section p-4 space-y-4 slide-up">
                <div class="bg-purple-600 text-white p-4 rounded-xl shadow-md flex items-center gap-3">
                    <i data-lucide="folder-open" class="w-8 h-8"></i>
                    <div><h2 class="text-xl font-bold">매뉴얼 및 도면</h2></div>
                </div>
                <div class="bg-white rounded-xl shadow-sm border border-gray-200 overflow-hidden divide-y divide-gray-100" id="manual-links-container">
                    <!-- JS로 동적 생성됨 -->
                </div>
            </section>

            <!-- 5. SSV 복귀 방법 (ssvReset) -->
            <section id="view-ssvReset" class="view-section p-4 space-y-4 slide-up">
                <div class="bg-green-600 text-white p-4 rounded-xl shadow-md flex items-center gap-3">
                    <i data-lucide="refresh-cw" class="w-8 h-8"></i>
                    <div>
                        <h2 class="text-xl font-bold">SSV / OPSO 복귀</h2>
                        <p class="text-green-100 text-sm">초보자를 위한 단계별 상세 복귀 가이드</p>
                    </div>
                </div>
                <div class="bg-yellow-50 border-l-4 border-yellow-500 p-4 rounded-r-lg mb-4">
                    <p class="text-sm text-yellow-800 font-bold flex items-center gap-2">
                        <i data-lucide="alert-triangle" class="w-4 h-4"></i> 가장 중요한 공통 주의사항
                    </p>
                    <p class="text-xs text-yellow-700 mt-1">
                        모든 밸브를 열 때는 압력이 급격히 차는 것을 막기 위해 <strong>"아주 미세하고 서서히"</strong> 열어야 합니다. 아래 라인(예비 정압기)에 문제가 생겼을 때도 동일한 순서로 작업합니다.
                    </p>
                </div>

                <div class="space-y-4">
                    <!-- 일반 SSV -->
                    <details class="bg-white rounded-lg shadow-sm border border-gray-200 group" open>
                        <summary class="font-bold p-4 cursor-pointer flex justify-between items-center text-gray-800 bg-gray-50 rounded-t-lg select-none">
                            1. 일반 SSV 복귀 순서 상세 가이드
                            <i data-lucide="chevron-down" class="text-green-500 group-open:rotate-180 transition-transform w-5 h-5"></i>
                        </summary>
                        <div class="p-4 border-t border-gray-200 text-sm text-gray-700 space-y-6">
                            <a href="https://drive.google.com/file/d/14kRzLSZx-_5W_U290f3jBJOwmKvUxRlf/view?usp=sharing" target="_blank" rel="noopener noreferrer" class="flex items-center justify-between p-3 bg-green-50 rounded-lg border border-green-200 hover:bg-green-100 active:bg-green-200 transition-colors">
                                <div class="flex items-center gap-3">
                                    <div class="bg-green-500 p-2 rounded-lg"><i data-lucide="file-text" class="w-4 h-4 text-white"></i></div>
                                    <div>
                                        <p class="font-bold text-green-900 text-sm">일반 SSV 설치 도면 보기</p>
                                        <p class="text-xs text-green-700">PDF 8-7-1 밸브 위치 참조</p>
                                    </div>
                                </div>
                                <i data-lucide="external-link" class="w-4 h-4 text-green-600"></i>
                            </a>
                            <div>
                                <h4 class="font-bold text-green-700 text-base mb-3 flex items-center gap-2">
                                    <span class="bg-green-100 text-green-700 px-2 py-0.5 rounded text-xs">1단계</span> 가스 유입 차단 (안전 확보)
                                </h4>
                                <div class="space-y-3 pl-2 border-l-2 border-green-100">
                                    <p><strong>1) 입구측 메인 밸브(1번) 닫기:</strong> 가스가 더 이상 들어오지 못하게 완전히 차단합니다.</p>
                                    <p><strong>2) 정압기 센싱 라인 밸브(7번) 닫기:</strong> 급격한 압력 변화를 막기 위해 아주 서서히 닫아줍니다.</p>
                                    <p><strong>3) 출구측 메인 밸브(2번) 닫기:</strong> 나가는 가스 길을 서서히 닫아 압력을 가둡니다.</p>
                                    <p><strong>4) SSV 센싱 라인 밸브(3번) 닫기:</strong> SSV가 더 이상 압력을 감지하지 않도록 차단합니다.</p>
                                </div>
                            </div>
                            <div>
                                <h4 class="font-bold text-green-700 text-base mb-3 flex items-center gap-2">
                                    <span class="bg-green-100 text-green-700 px-2 py-0.5 rounded text-xs">2단계</span> 압력 제거 및 레버 복귀
                                </h4>
                                <div class="space-y-3 pl-2 border-l-2 border-green-100">
                                    <p><strong>5) 잔류가스 방출:</strong> 방출 밸브(4번)를 열어 SSV 내부에 남은 가스를 "쉬익" 소리가 멈출 때까지 완전히 빼낸 뒤 다시 닫습니다.</p>
                                    <p><strong>6) 압력 평형 맞추기:</strong> 이퀄라이징 밸브(5번)를 열어 SSV 앞뒤의 압력을 똑같이 맞춰줍니다. (이 과정이 있어야 레버가 움직입니다.) 평형이 맞춰지면 밸브를 다시 닫습니다.</p>
                                    <p class="bg-green-50 p-2 rounded text-green-800">
                                        <strong>7) 기기 복귀:</strong> SSV 본체에 달린 복귀 레버(6번)를 잡고 화살표 방향으로 90도 회전시킵니다. <strong>"딱!" 하는 경쾌한 걸림 소리</strong>가 나면 기기가 정상적으로 복귀된 것입니다.
                                    </p>
                                </div>
                            </div>
                            <div>
                                <h4 class="font-bold text-green-700 text-base mb-3 flex items-center gap-2">
                                    <span class="bg-green-100 text-green-700 px-2 py-0.5 rounded text-xs">3단계</span> 안전 재가동 (매우 서서히)
                                </h4>
                                <div class="space-y-3 pl-2 border-l-2 border-green-100">
                                    <p><strong>8) 출구측 메인 밸브(2번) 개방:</strong> 다시 가스가 나갈 수 있도록 서서히 열어줍니다.</p>
                                    <p><strong>9) 정압기 & SSV 센싱 개방:</strong> 정압기 센싱 라인(7번)과 SSV 센싱 라인(3번) 밸브를 순서대로 서서히 열어 압력 감지 기능을 살립니다.</p>
                                    <p class="text-red-600 font-medium">
                                        <strong>10) 입구측 미세 개방 (중요):</strong> 입구측 밸브(1번)를 열 차례입니다. 반드시 출구측 압력계(8번)의 바늘을 뚫어져라 주시하며, 목표한 설정 압력까지 천천히 차오르도록 밸브를 <strong>아주 미세하게</strong> 엽니다.
                                    </p>
                                    <p><strong>11) 최종 개방:</strong> 출구측 압력계가 설정 압력에 도달하면, <strong>속으로 10초 정도를 세며 안정화되는지 지켜본 뒤</strong> 밸브를 완전히 활짝 엽니다.</p>
                                </div>
                            </div>
                        </div>
                    </details>

                    <!-- OPSO -->
                    <details class="bg-white rounded-lg shadow-sm border border-gray-200 group">
                        <summary class="font-bold p-4 cursor-pointer flex justify-between items-center text-gray-800 bg-gray-50 rounded-t-lg select-none">
                            2. OPSO 복귀 상세 가이드 (299HS 우)
                            <i data-lucide="chevron-down" class="text-green-500 group-open:rotate-180 transition-transform w-5 h-5"></i>
                        </summary>
                        <div class="p-4 border-t border-gray-200 text-sm text-gray-700 space-y-6">
                            <a href="https://drive.google.com/file/d/1s6Q0lGQVjndnQSaE37lr36kqnh8RPf4Q/view?usp=sharing" target="_blank" rel="noopener noreferrer" class="flex items-center justify-between p-3 bg-gray-50 rounded-lg border border-gray-200 hover:bg-gray-100 active:bg-gray-200 transition-colors mb-4">
                                <div class="flex items-center gap-3">
                                    <div class="bg-gray-400 p-2 rounded-lg"><i data-lucide="file-text" class="w-4 h-4 text-white"></i></div>
                                    <div>
                                        <p class="font-bold text-gray-700 text-sm">OPSO 설치 도면 보기</p>
                                        <p class="text-xs text-gray-500">PDF 8-8-1 밸브 위치 참조</p>
                                    </div>
                                </div>
                                <i data-lucide="external-link" class="w-4 h-4 text-gray-400"></i>
                            </a>
                            <div>
                                <h4 class="font-bold text-green-700 text-base mb-3 flex items-center gap-2">
                                    <span class="bg-green-100 text-green-700 px-2 py-0.5 rounded text-xs">1단계</span> 차단 및 필터 가스 방출
                                </h4>
                                <div class="space-y-3 pl-2 border-l-2 border-green-100">
                                    <p><strong>1) 라인 차단:</strong> 입구측 메인 밸브(1번)를 완전히 닫아 가스를 막습니다.</p>
                                    <p><strong>2) 센싱 및 출구 차단:</strong> 센싱 라인 밸브(5번)와 출구측 메인 밸브(2번)를 순서대로 서서히 닫습니다.</p>
                                    <p><strong>3) 내부 가스 방출:</strong> 방출 밸브(3번)를 서서히 열어 필터와 배관 내부에 갇힌 가스를 안전하게 모두 빼낸 후 밸브를 다시 닫아줍니다.</p>
                                </div>
                            </div>
                            <div>
                                <h4 class="font-bold text-green-700 text-base mb-3 flex items-center gap-2">
                                    <span class="bg-green-100 text-green-700 px-2 py-0.5 rounded text-xs">2단계</span> 기기 복귀 (레버 조작)
                                </h4>
                                <div class="space-y-3 pl-2 border-l-2 border-green-100">
                                    <p class="bg-green-50 p-2 rounded text-green-800">
                                        <strong>4) OPSO 레버 복귀:</strong> OPSO 복귀 레버(4번)를 잡고 <strong>시계 반대 방향</strong>으로 끝까지 돌립니다. 그 상태에서 레버를 아래로 가볍게 "딸깍" 당겨 복귀시킨 후, 조작했던 레버를 다시 원래 위치로 되돌려 놓습니다.
                                    </p>
                                </div>
                            </div>
                            <div>
                                <h4 class="font-bold text-green-700 text-base mb-3 flex items-center gap-2">
                                    <span class="bg-green-100 text-green-700 px-2 py-0.5 rounded text-xs">3단계</span> 재가동 (매우 서서히)
                                </h4>
                                <div class="space-y-3 pl-2 border-l-2 border-green-100">
                                    <p><strong>5) 출구측 미세 개방:</strong> 출구측 밸브(2번)를 가스가 아주 조금만(최소 유량) 흐를 수 있을 정도로만 살짝 엽니다.</p>
                                    <p><strong>6) 센싱 개방:</strong> 센싱 라인 밸브(5번)를 서서히 열어 감지 기능을 살립니다.</p>
                                    <p class="text-red-600 font-medium">
                                        <strong>7) 입구측 개방 (중요):</strong> 입구측 밸브(1번)를 열며 출구측 압력계(6번)를 계속 주시합니다. 바늘이 목표 압력에 서서히 도달하도록 밸브를 아주 조금씩 엽니다.
                                    </p>
                                    <p><strong>8) 최종 개방:</strong> 출구 압력이 설정 압력에 도달하면, <strong>약 5~10초 정도 여유를 두고 기다리며</strong> 정상 유지되는지 확인한 뒤 밸브를 서서히 완전히 끝까지 개방합니다.</p>
                                </div>
                            </div>
                        </div>
                    </details>
                </div>
            </section>

            <!-- 6. 일일 안전 점검 (checklist) -->
            <section id="view-checklist" class="view-section p-4 space-y-4 slide-up">
                <div class="bg-teal-600 text-white p-4 rounded-xl shadow-md flex items-center gap-3">
                    <i data-lucide="shield-check" class="w-8 h-8"></i>
                    <div>
                        <h2 class="text-xl font-bold">일일 안전 점검표</h2>
                        <p class="text-teal-100 text-sm">정압기실 및 RTU 필수 확인 항목</p>
                    </div>
                </div>

                <div class="bg-white rounded-xl shadow-sm border border-gray-200 overflow-hidden divide-y divide-gray-100">
                    <div class="bg-gray-50 p-3 text-xs font-bold text-gray-500 flex justify-between items-center">
                        <span>체크리스트 진행도</span>
                        <span class="text-teal-600"><span id="chk-count">0</span> / 8</span>
                    </div>
                    <div class="w-full bg-gray-200 h-1.5">
                        <div id="chk-progress" class="bg-teal-500 h-1.5 transition-all duration-300" style="width: 0%;"></div>
                    </div>
                    <div class="p-2" id="checklist-container">
                        <!-- JS로 동적 생성됨 -->
                    </div>
                </div>

                <button id="btn-submit" onclick="submitChecklist()" class="w-full py-4 rounded-xl font-bold text-white shadow-md transition-all bg-gray-300 cursor-not-allowed">
                    모든 항목을 점검해 주세요
                </button>
            </section>

            <!-- 7. 비상 연락망 (contact) -->
            <section id="view-contact" class="view-section p-4 space-y-4 slide-up">
                <div class="bg-gray-800 text-white p-4 rounded-xl shadow-md flex items-center gap-3">
                    <i data-lucide="phone-call" class="w-8 h-8"></i>
                    <div>
                        <h2 class="text-xl font-bold">비상 연락망</h2>
                        <p class="text-gray-300 text-sm">긴급 출동 및 관계자 직통 연결</p>
                    </div>
                </div>

                <div class="space-y-4">
                    <div>
                        <h3 class="text-sm font-bold text-red-600 ml-1 mb-2">🚨 긴급 출동 (사고 발생 시)</h3>
                        <div class="bg-white rounded-xl shadow-sm border border-red-100 overflow-hidden divide-y divide-gray-100">
                            <a href="tel:063-119" class="flex items-center justify-between p-4 hover:bg-red-50 active:bg-red-100 transition-colors">
                                <div><p class="font-bold text-gray-800 text-lg">소방서 지휘통제실</p><p class="text-sm text-red-500 font-mono">063-119</p></div>
                                <div class="bg-red-100 text-red-700 p-2.5 rounded-full"><i data-lucide="phone-call" class="w-5 h-5"></i></div>
                            </a>
                            <a href="tel:063-112" class="flex items-center justify-between p-4 hover:bg-red-50 active:bg-red-100 transition-colors">
                                <div><p class="font-bold text-gray-800 text-lg">경찰서 민원접수실</p><p class="text-sm text-red-500 font-mono">063-112</p></div>
                                <div class="bg-red-100 text-red-700 p-2.5 rounded-full"><i data-lucide="phone-call" class="w-5 h-5"></i></div>
                            </a>
                            <a href="tel:063-440-7788" class="flex items-center justify-between p-4 hover:bg-red-50 active:bg-red-100 transition-colors">
                                <div><p class="font-bold text-gray-800 text-lg">상황실</p><p class="text-sm text-red-500 font-mono">063-440-7788</p></div>
                                <div class="bg-red-100 text-red-700 p-2.5 rounded-full"><i data-lucide="phone-call" class="w-5 h-5"></i></div>
                            </a>
                        </div>
                    </div>
                    <div>
                        <h3 class="text-sm font-bold text-blue-700 ml-1 mb-2">👨‍🔧 관리 감독 및 책임자</h3>
                        <div class="bg-white rounded-xl shadow-sm border border-blue-100 overflow-hidden divide-y divide-gray-100">
                            <a href="tel:010-5605-1862" class="flex items-center justify-between p-4 hover:bg-blue-50 active:bg-blue-100 transition-colors">
                                <div>
                                    <p class="font-bold text-gray-800">김하중 팀장</p>
                                    <p class="text-sm text-gray-500">안전관리 책임자</p>
                                    <p class="text-sm text-blue-600 font-mono mt-0.5">010-5605-1862</p>
                                </div>
                                <div class="bg-blue-100 text-blue-700 p-2.5 rounded-full"><i data-lucide="phone-call" class="w-5 h-5"></i></div>
                            </a>
                            <a href="tel:010-7258-2015" class="flex items-center justify-between p-4 hover:bg-blue-50 active:bg-blue-100 transition-colors">
                                <div>
                                    <p class="font-bold text-gray-800">이재용 주무관</p>
                                    <p class="text-sm text-gray-500">군산시 에너지과</p>
                                    <p class="text-sm text-blue-600 font-mono mt-0.5">010-7258-2015</p>
                                </div>
                                <div class="bg-blue-100 text-blue-700 p-2.5 rounded-full"><i data-lucide="phone-call" class="w-5 h-5"></i></div>
                            </a>
                        </div>
                    </div>
                </div>
            </section>
        </main>

        <!-- 모달: 점검 제출 완료 팝업 -->
        <div id="modal-submit" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/50 backdrop-blur-sm hidden">
            <div class="bg-white rounded-2xl shadow-xl w-full max-w-sm overflow-hidden fade-in">
                <div class="bg-teal-500 p-6 flex flex-col items-center justify-center relative">
                    <button onclick="closeSubmitModal()" class="absolute top-3 right-3 text-teal-100 hover:text-white transition-colors">
                        <i data-lucide="x" class="w-5 h-5"></i>
                    </button>
                    <div class="bg-white p-3 rounded-full mb-3 shadow-sm">
                        <i data-lucide="check-circle-2" class="w-10 h-10 text-teal-500"></i>
                    </div>
                    <h3 class="text-xl font-bold text-white mb-1">점검 제출 완료</h3>
                </div>
                <div class="p-6 text-center bg-white">
                    <p class="text-gray-800 font-medium text-lg mb-2">수고하셨습니다.</p>
                    <p class="text-sm text-gray-500">일일 안전 점검 내역이<br/>시스템에 정상적으로 기록되었습니다.</p>
                    <button onclick="closeSubmitModalAndHome()" class="mt-6 w-full py-3 bg-gray-100 hover:bg-gray-200 active:bg-gray-300 text-gray-800 font-bold rounded-xl transition-colors">
                        확인
                    </button>
                </div>
            </div>
        </div>

        <!-- 모달: 정압기 상세 정보 팝업 -->
        <div id="modal-info" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/50 backdrop-blur-sm hidden">
            <div class="bg-white rounded-2xl shadow-xl w-full max-w-sm overflow-hidden flex flex-col max-h-[80vh] fade-in">
                <div class="bg-blue-600 p-4 flex justify-between items-center sticky top-0 z-10">
                    <h3 class="text-lg font-bold text-white flex items-center gap-2">
                        <i data-lucide="info" class="w-5 h-5"></i> 개정통사 정압기 상세 제원
                    </h3>
                    <button onclick="closeInfoPopup()" class="text-blue-100 hover:text-white transition-colors p-1">
                        <i data-lucide="x" class="w-6 h-6"></i>
                    </button>
                </div>
                <div class="p-4 overflow-y-auto">
                    <div class="divide-y divide-gray-100 border border-gray-100 rounded-lg" id="specs-container">
                        <!-- JS로 동적 생성됨 -->
                    </div>
                </div>
                <div class="p-4 bg-gray-50 border-t border-gray-100">
                    <button onclick="closeInfoPopup()" class="w-full py-3 bg-blue-600 hover:bg-blue-700 active:bg-blue-800 text-white font-bold rounded-xl transition-colors shadow-sm">
                        닫기
                    </button>
                </div>
            </div>
        </div>

    </div>

    <script>
        // Lucide 아이콘 초기화
        lucide.createIcons();

        // 뷰 이동 함수
        function changeView(viewId) {
            document.querySelectorAll('.view-section').forEach(el => el.classList.remove('active'));
            document.getElementById('view-' + viewId).classList.add('active');
            
            const backBtn = document.getElementById('btn-back');
            if (viewId === 'home') {
                backBtn.classList.add('hidden');
            } else {
                backBtn.classList.remove('hidden');
            }
            window.scrollTo(0, 0); // 화면 최상단으로
        }

        // --- 매뉴얼 링크 동적 생성 ---
        const manualLinksData = [
            { category: "장비 매뉴얼", title: "정압기 종합 운영 매뉴얼 (PDF)", url: "#" },
            { category: "장비 매뉴얼", title: "AFV 가스 밸브 유지보수 가이드", url: "#" },
            { category: "장비 매뉴얼", title: "필터(Filter) 엘리먼트 교체 및 정비 매뉴얼", url: "#" },
            { category: "장비 매뉴얼", title: "안전차단밸브(SSV) 정밀 세팅 가이드", url: "#" },
            { category: "장비 매뉴얼", title: "이상압력발생방지장치(Relief Valve) 매뉴얼", url: "#" },
            { category: "장비 매뉴얼", title: "가스누출검지기(Gas Detector) 캘리브레이션", url: "#" },
            { category: "장비 매뉴얼", title: "온수보일러(Water Bath Heater) 취급 설명서", url: "#" },
            { category: "기술 도면", title: "배관망 P&ID 도면 (고해상도)", url: "#" },
            { category: "기술 도면", title: "정압기실 건축 평면도 및 단면도", url: "#" },
            { category: "기술 도면", title: "정압기 전기 제어 판넬 회로도", url: "#" },
            { category: "기술 도면", title: "RTU 통신 및 원격 감시 설비 계통도", url: "#" },
            { category: "기술 도면", title: "가스 배관 아이소메트릭(Isometric) 도면", url: "#" },
            { category: "안전 규정", title: "밀폐공간 출입 및 작업 안전 수칙", url: "#" },
            { category: "안전 규정", title: "방폭 구역 내 화기 취급 작업 지침", url: "#" },
            { category: "안전 규정", title: "가스 질식 사고 대비 응급 처치 매뉴얼", url: "#" },
            { category: "안전 규정", title: "동절기 정압기실 동파 방지 관리 기준", url: "#" },
            { category: "안전 규정", title: "KGS Code FS551 (정압기 시설 기준)", url: "#" },
            { category: "점검 양식", title: "일일/주간/월간 정압기 순회 점검표", url: "#" },
            { category: "점검 양식", title: "가스 누출 의심 시 긴급 출동 보고서", url: "#" },
            { category: "점검 양식", title: "소모품(오링, 가스켓, 필터) 교체 이력 대장", url: "#" }
        ];

        const linksContainer = document.getElementById('manual-links-container');
        manualLinksData.forEach(item => {
            const a = document.createElement('a');
            a.href = item.url;
            a.className = "flex items-center p-4 hover:bg-gray-50 active:bg-gray-100 group";
            a.innerHTML = `
                <div class="bg-purple-100 p-2 rounded-lg mr-4 flex-shrink-0 group-hover:bg-purple-200">
                    <i data-lucide="file-text" class="w-5 h-5 text-purple-700"></i>
                </div>
                <div class="flex-1 min-w-0">
                    <p class="text-xs text-gray-500 mb-0.5">${item.category}</p>
                    <p class="text-sm font-bold text-gray-800 truncate">${item.title}</p>
                </div>
            `;
            linksContainer.appendChild(a);
        });

        // --- 일일 점검표 기능 ---
        const checklistData = [
            { id: 1, text: "가스 누출 검지 (연결부위, 밸브류 등 비눗물/검지기 확인)" },
            { id: 2, text: "압력계 지시치 확인 (입구/출구 압력이 정상 범위 내인가?)" },
            { id: 3, text: "필터 차압계 확인" },
            { id: 4, text: "SSV 및 Relief 밸브 외관, 벤트라인, 도색 상태 이상 유무" },
            { id: 5, text: "RTU 통신 상태 및 배터리 전압(충전상태) 확인" },
            { id: 6, text: "혹서기 RTU팬 작동 여부 확인" },
            { id: 7, text: "정압기실 내부 환기구 막힘, 냄새 유무 및 강제배기팬 작동" },
            { id: 8, text: "정압기실 주변 지반 침하, 침수, 화기 등 위험요인 유무" }
        ];

        let checkedState = [];
        const chkContainer = document.getElementById('checklist-container');
        const chkCountSpan = document.getElementById('chk-count');
        const chkProgress = document.getElementById('chk-progress');
        const btnSubmit = document.getElementById('btn-submit');

        function renderChecklist() {
            chkContainer.innerHTML = '';
            checklistData.forEach(item => {
                const isChecked = checkedState.includes(item.id);
                const btn = document.createElement('button');
                btn.className = `w-full flex items-start gap-3 p-3 text-left transition-colors rounded-lg ${isChecked ? 'bg-teal-50' : 'hover:bg-gray-50 active:bg-gray-100'}`;
                btn.onclick = () => toggleCheck(item.id);
                
                const iconHTML = isChecked 
                    ? `<i data-lucide="check-circle-2" class="w-6 h-6 text-teal-600"></i>`
                    : `<i data-lucide="circle" class="w-6 h-6 text-gray-300"></i>`;
                
                const textClass = isChecked ? 'text-teal-900 font-medium' : 'text-gray-700';

                btn.innerHTML = `
                    <div class="mt-0.5 flex-shrink-0">${iconHTML}</div>
                    <span class="text-sm ${textClass}">${item.text}</span>
                `;
                chkContainer.appendChild(btn);
            });
            lucide.createIcons();

            // 진행도 업데이트
            chkCountSpan.innerText = checkedState.length;
            chkProgress.style.width = `${(checkedState.length / checklistData.length) * 100}%`;

            // 제출 버튼 활성화
            if (checkedState.length === checklistData.length) {
                btnSubmit.className = "w-full py-4 rounded-xl font-bold text-white shadow-md transition-all bg-teal-600 hover:bg-teal-700 active:bg-teal-800";
                btnSubmit.innerText = "점검 완료 및 제출";
            } else {
                btnSubmit.className = "w-full py-4 rounded-xl font-bold text-white shadow-md transition-all bg-gray-300 cursor-not-allowed";
                btnSubmit.innerText = "모든 항목을 점검해 주세요";
            }
        }

        function toggleCheck(id) {
            if (checkedState.includes(id)) {
                checkedState = checkedState.filter(item => item !== id);
            } else {
                checkedState.push(id);
            }
            renderChecklist();
        }

        function submitChecklist() {
            if (checkedState.length === checklistData.length) {
                document.getElementById('modal-submit').classList.remove('hidden');
            }
        }

        function closeSubmitModal() {
            document.getElementById('modal-submit').classList.add('hidden');
        }

        function closeSubmitModalAndHome() {
            closeSubmitModal();
            checkedState = []; // 초기화
            renderChecklist();
            changeView('home');
        }

        // 초기 렌더링
        renderChecklist();

        // --- 정압기 제원 팝업 기능 ---
        const governorSpecs = [
            { label: "모델", value: '1098EGR 3"' },
            { label: "제조", value: "선일" },
            { label: "중압", value: "100A" },
            { label: "저압", value: "315mm" },
            { label: "필터 / 오픈", value: "G2.5 / 퀵오픈" },
            { label: "SSV", value: "JEQ(31인치)" },
            { label: "소음기", value: "위스퍼케이지, 위스퍼케이지" },
            { label: "구조물", value: "케비넷" },
            { label: "RTU", value: "SmartRTU(바스파워텍)" },
            { label: "UPS", value: "SmartRTU(바스파워텍)" },
            { label: "가스경보기", value: "ND-205B" },
            { label: "SSV센서", value: "NJ 시리즈" },
            { label: "서지보호기", value: "GPS-I-220A" },
            { label: "모뎀", value: "MXR-40KD" },
            { label: "압력계", value: "1차 WISE / 2차 WISE" }
        ];

        const specsContainer = document.getElementById('specs-container');
        governorSpecs.forEach(spec => {
            const div = document.createElement('div');
            div.className = "py-2.5 px-3 flex justify-between items-center text-sm bg-white even:bg-gray-50";
            div.innerHTML = `
                <span class="text-gray-500 font-medium whitespace-nowrap mr-4">${spec.label}</span>
                <span class="text-gray-900 font-bold text-right break-words">${spec.value}</span>
            `;
            specsContainer.appendChild(div);
        });

        function openInfoPopup() {
            document.getElementById('modal-info').classList.remove('hidden');
        }

        function closeInfoPopup() {
            document.getElementById('modal-info').classList.add('hidden');
        }

    </script>
</body>
</html>
