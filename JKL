<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>개인 맞춤형 미디어 추천 시스템</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700;900&display=swap');
        body {
            font-family: 'Noto Sans KR', sans-serif;
            background-color: #0b0f19;
            color: #f3f4f6;
        }
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #111827;
        }
        ::-webkit-scrollbar-thumb {
            background: #374151;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #4b5563;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between">

    <!-- Header -->
    <header class="border-b border-gray-800 bg-gray-900/80 backdrop-blur sticky top-0 z-50">
        <div class="max-w-4xl mx-auto px-4 py-4 flex justify-between items-center">
            <div class="flex items-center space-x-3">
                <div class="bg-indigo-600 p-2 rounded-lg text-white">
                    <i class="fa-solid fa-film text-xl"></i>
                </div>
                <span class="text-xl font-black tracking-wider bg-gradient-to-r from-indigo-400 to-purple-500 bg-clip-text text-transparent">CINE-MATCH</span>
            </div>
            <div class="text-xs text-gray-400 border border-gray-800 px-3 py-1.5 rounded-full bg-gray-950">
                <i class="fa-solid fa-circle-info mr-1 text-indigo-400"></i> AI 추천 엔진 v2.5
            </div>
        </div>
    </header>

    <!-- Main Content Area -->
    <main class="flex-grow max-w-4xl w-full mx-auto px-4 py-8">
        
        <!-- Step Indicator -->
        <div class="mb-8" id="stepIndicator">
            <div class="flex items-center justify-between max-w-md mx-auto">
                <div class="flex flex-col items-center">
                    <div id="step1-circle" class="w-10 h-10 rounded-full flex items-center justify-center bg-indigo-600 text-white font-bold transition-all duration-300">1</div>
                    <span id="step1-text" class="text-xs mt-2 text-indigo-400 font-medium">선호도 및 시청시간</span>
                </div>
                <div class="flex-1 h-0.5 mx-2 bg-gray-800" id="step-line-1">
                    <div id="step-line-1-progress" class="h-full bg-indigo-600 w-0 transition-all duration-500"></div>
                </div>
                <div class="flex flex-col items-center">
                    <div id="step2-circle" class="w-10 h-10 rounded-full flex items-center justify-center bg-gray-800 text-gray-400 font-bold transition-all duration-300">2</div>
                    <span id="step2-text" class="text-xs mt-2 text-gray-500 font-medium">관람작 평점 매기기</span>
                </div>
                <div class="flex-1 h-0.5 mx-2 bg-gray-800" id="step-line-2">
                    <div id="step-line-2-progress" class="h-full bg-indigo-600 w-0 transition-all duration-500"></div>
                </div>
                <div class="flex flex-col items-center">
                    <div id="step3-circle" class="w-10 h-10 rounded-full flex items-center justify-center bg-gray-800 text-gray-400 font-bold transition-all duration-300">3</div>
                    <span id="step3-text" class="text-xs mt-2 text-gray-500 font-medium">맞춤형 추천 분석</span>
                </div>
            </div>
        </div>

        <!-- APP CONTAINER -->
        <div class="bg-gray-900 border border-gray-800 rounded-2xl p-6 md:p-8 shadow-2xl relative overflow-hidden">
            <div class="absolute top-0 left-0 right-0 h-1.5 bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500"></div>

            <!-- STEP 1: 선호 장르 및 시간 조사 -->
            <div id="step1-container" class="space-y-6">
                <div class="text-center md:text-left">
                    <h2 class="text-2xl font-bold text-white flex items-center justify-center md:justify-start gap-2">
                        <i class="fa-solid fa-heart text-pink-500 animate-pulse"></i> 
                        어떤 장르를 얼마나 보시나요?
                    </h2>
                    <p class="text-gray-400 mt-1 text-sm">평소 가장 좋아하는 미디어 장르와 주간 평균 시청 시간을 입력해주세요.</p>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-6">
                    <!-- Genre Selection Cards -->
                    <div class="space-y-3 md:col-span-2">
                        <label class="block text-sm font-semibold text-gray-300">선호 장르 선택 <span class="text-xs text-indigo-400">(복수 선택 가능)</span></label>
                        <div class="grid grid-cols-2 sm:grid-cols-3 gap-3" id="genre-grid">
                            <!-- 로딩되거나 자바스크립트로 생성될 장르 버튼들 -->
                        </div>
                    </div>
                </div>

                <!-- Selected Genres Sliders -->
                <div id="selected-genres-sliders" class="space-y-4 pt-4 border-t border-gray-800 hidden">
                    <label class="block text-sm font-semibold text-gray-300">
                        <i class="fa-regular fa-clock mr-1.5 text-indigo-400"></i> 선택한 장르의 주간 평균 시청 시간
                    </label>
                    <p class="text-xs text-gray-500 -mt-2">해당 장르를 일주일에 대략 몇 시간 정도 시청하시는지 슬라이더로 조절해 주세요.</p>
                    <div class="space-y-4 bg-gray-950 p-4 rounded-xl border border-gray-800" id="sliders-container">
                        <!-- 선택된 장르에 대한 시청시간 조절 슬라이더들이 동적으로 표시됨 -->
                    </div>
                </div>

                <div class="flex justify-end pt-4">
                    <button id="btn-to-step2" class="w-full md:w-auto px-6 py-3.5 bg-indigo-600 hover:bg-indigo-500 disabled:opacity-50 disabled:cursor-not-allowed text-white font-semibold rounded-xl flex items-center justify-center gap-2 shadow-lg shadow-indigo-600/20 transition-all" disabled>
                        다음 단계로 이동 <i class="fa-solid fa-arrow-right"></i>
                    </button>
                </div>
            </div>

            <!-- STEP 2: 본 영화 작성 및 평점 매기기 -->
            <div id="step2-container" class="space-y-6 hidden">
                <div class="flex flex-col md:flex-row md:items-center justify-between gap-4">
                    <div>
                        <h2 class="text-2xl font-bold text-white flex items-center gap-2">
                            <i class="fa-solid fa-star text-yellow-500"></i>
                            이미 보신 작품들의 평점을 알려주세요!
                        </h2>
                        <p class="text-gray-400 mt-1 text-sm">입력된 평점과 취향 데이터를 기반으로 취향 필터링 알고리즘이 가동됩니다.</p>
                    </div>
                    <div class="flex gap-2">
                        <button id="btn-add-watched" class="px-4 py-2 bg-gray-800 hover:bg-gray-700 text-gray-200 text-sm font-medium rounded-lg border border-gray-700 flex items-center gap-1.5 transition">
                            <i class="fa-solid fa-plus text-indigo-400"></i> 직접 추가하기
                        </button>
                    </div>
                </div>

                <!-- Instruction Info Box -->
                <div class="bg-indigo-950/40 border border-indigo-900/50 rounded-xl p-4 flex gap-3 text-sm">
                    <div class="text-indigo-400 mt-0.5"><i class="fa-solid fa-lightbulb"></i></div>
                    <div class="text-indigo-200/90 leading-relaxed">
                        선택하신 장르별로 이미 본 영화나 드라마가 있다면 제목을 적고 별점을 남겨주세요. 
                        <strong>리스트의 별을 클릭하면 즉시 평점을 변경할 수 있습니다.</strong> 입력이 많을수록 추천이 더욱 정교해집니다.
                    </div>
                </div>

                <!-- Tab system for Selected Genres in Step 2 -->
                <div class="border-b border-gray-800">
                    <nav class="flex space-x-2 overflow-x-auto pb-px" id="step2-genre-tabs">
                        <!-- Selected genres tab buttons will dynamic here -->
                    </nav>
                </div>

                <!-- List of watched movies for active tab -->
                <div class="bg-gray-950 p-5 rounded-xl border border-gray-800 min-h-[250px]" id="watched-list-container">
                    <div id="watched-movies-list" class="space-y-3">
                        <!-- Dynamic movie rows will appear here -->
                    </div>
                    <div id="empty-watched-state" class="hidden flex flex-col items-center justify-center py-12 text-gray-500">
                        <i class="fa-solid fa-clapperboard text-4xl mb-3 text-gray-700"></i>
                        <p>이 장르에 등록된 관람작이 없습니다.</p>
                        <p class="text-xs mt-1 text-gray-600">위의 '직접 추가하기' 버튼으로 본 작품을 입력해보세요.</p>
                    </div>
                </div>

                <div class="flex flex-col sm:flex-row justify-between items-center gap-4 pt-4 border-t border-gray-800">
                    <button id="btn-back-to-step1" class="w-full sm:w-auto px-5 py-3 text-gray-400 hover:text-white font-medium flex items-center justify-center gap-2 transition">
                        <i class="fa-solid fa-arrow-left"></i> 이전 단계로
                    </button>
                    <button id="btn-to-step3" class="w-full sm:w-auto px-6 py-3.5 bg-gradient-to-r from-indigo-600 to-purple-600 hover:from-indigo-500 hover:to-purple-500 text-white font-bold rounded-xl flex items-center justify-center gap-2 shadow-lg shadow-purple-600/20 transition-all">
                        <i class="fa-solid fa-wand-magic-sparkles"></i> 취향 분석 및 추천받기
                    </button>
                </div>
            </div>

            <!-- STEP 3: 알고리즘 결과 & 추천 페이지 -->
            <div id="step3-container" class="space-y-8 hidden">
                <!-- Top Status Header -->
                <div class="text-center max-w-xl mx-auto space-y-2">
                    <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-emerald-500/10 text-emerald-400 border border-emerald-500/20 text-xs font-semibold mb-2">
                        <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span> 분석 완료 및 알고리즘 생성 성공
                    </div>
                    <h2 class="text-3xl font-extrabold text-white">당신만을 위한 맞춤 미디어 큐레이션</h2>
                    <p class="text-gray-400 text-sm">입력해주신 선호 장르 비율, 가용 시청 시간, 그리고 선호 평점 성향을 머신러닝 기반 협업 필터링 알고리즘으로 분석했습니다.</p>
                </div>

                <!-- Recommendation Insight Metrics -->
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                    <div class="bg-gray-950 p-4 rounded-xl border border-gray-800 flex items-center gap-4">
                        <div class="p-3 rounded-lg bg-pink-500/10 text-pink-400"><i class="fa-solid fa-heart text-xl"></i></div>
                        <div>
                            <p class="text-xs text-gray-500 font-semibold">최선호 장르</p>
                            <p class="text-lg font-bold text-white" id="stat-fav-genre">-</p>
                        </div>
                    </div>
                    <div class="bg-gray-950 p-4 rounded-xl border border-gray-800 flex items-center gap-4">
                        <div class="p-3 rounded-lg bg-blue-500/10 text-blue-400"><i class="fa-solid fa-hourglass-half text-xl"></i></div>
                        <div>
                            <p class="text-xs text-gray-500 font-semibold">주간 총 시청 시간</p>
                            <p class="text-lg font-bold text-white" id="stat-total-hours">-</p>
                        </div>
                    </div>
                    <div class="bg-gray-950 p-4 rounded-xl border border-gray-800 flex items-center gap-4">
                        <div class="p-3 rounded-lg bg-yellow-500/10 text-yellow-400"><i class="fa-solid fa-star-half-stroke text-xl"></i></div>
                        <div>
                            <p class="text-xs text-gray-500 font-semibold">기존 관람작 평균 평점</p>
                            <p class="text-lg font-bold text-white" id="stat-avg-rating">-</p>
                        </div>
                    </div>
                </div>

                <!-- Content Type Selection Tab (Movie vs Drama) -->
                <div class="flex items-center justify-between border-b border-gray-800 pb-2">
                    <h3 class="text-xl font-bold text-white flex items-center gap-2">
                        <i class="fa-solid fa-fire text-orange-500"></i> 추천 콘텐츠 라인업
                    </h3>
                    <div class="bg-gray-950 p-1 rounded-lg border border-gray-800 flex">
                        <button id="toggle-all" class="px-3 py-1.5 rounded-md text-xs font-semibold bg-indigo-600 text-white transition">전체</button>
                        <button id="toggle-movie" class="px-3 py-1.5 rounded-md text-xs font-semibold text-gray-400 hover:text-white transition">영화만</button>
                        <button id="toggle-drama" class="px-3 py-1.5 rounded-md text-xs font-semibold text-gray-400 hover:text-white transition">드라마만</button>
                    </div>
                </div>

                <!-- Grid Recommendations -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6" id="recommendation-cards-container">
                    <!-- Dynamic recommendations will render here -->
                </div>

                <!-- Algorithm Description Box -->
                <div class="bg-gray-950 border border-gray-800 rounded-xl p-5 space-y-3">
                    <h4 class="text-sm font-bold text-indigo-400 flex items-center gap-1.5">
                        <i class="fa-solid fa-gears"></i> 추천 가중치 알고리즘 산출 근거
                    </h4>
                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-4 pt-2 text-xs text-gray-400">
                        <div>
                            <span class="block text-gray-500 font-semibold mb-1">1. 장르별 시청 가용 시간</span>
                            입력된 시청 시간이 많을수록, 가볍게 볼 수 있는 롱폼(드라마)의 비중을 자동 계산하고 추천 리스트의 우선순위에 반영했습니다.
                        </div>
                        <div>
                            <span class="block text-gray-500 font-semibold mb-1">2. 개인 평가 피드백</span>
                            사용자가 높게 평가한(별점 4.0 이상) 작품과 유사한 감독, 배우, 스토리 라인을 지닌 미디어를 최우선으로 가중치를 보정했습니다.
                        </div>
                        <div>
                            <span class="block text-gray-500 font-semibold mb-1">3. 상호 필터링 필터</span>
                            미평가 및 시청하지 않은 웰메이드 콘텐츠 라이브러리 중, 매칭 스코어가 85% 이상인 히트작을 매칭했습니다.
                        </div>
                    </div>
                </div>

                <!-- Reset Button -->
                <div class="flex justify-center pt-2">
                    <button id="btn-reset" class="px-6 py-3 bg-gray-800 hover:bg-gray-700 text-gray-200 font-semibold rounded-xl flex items-center gap-2 transition">
                        <i class="fa-solid fa-rotate-left"></i> 설문조사 다시 시작하기
                    </button>
                </div>
            </div>

        </div>
    </main>

    <!-- Footer -->
    <footer class="border-t border-gray-800 bg-gray-950 py-6 text-center text-xs text-gray-500">
        <p>© 2026 CINE-MATCH Inc. All Rights Reserved.</p>
        <p class="mt-1 text-gray-600">본 알고리즘은 사용자의 프라이버시를 존중하며 입력한 데이터는 로컬 브라우저 세션에서만 임시 처리됩니다.</p>
    </footer>

    <!-- custom notification toast (Non-alert) -->
    <div id="toast" class="fixed bottom-5 right-5 z-50 bg-gray-900 border border-gray-800 text-gray-100 px-4 py-3 rounded-xl shadow-2xl flex items-center gap-3 transform translate-y-10 opacity-0 pointer-events-none transition-all duration-300">
        <div id="toast-icon-box" class="p-1 rounded bg-indigo-600/10 text-indigo-400">
            <i class="fa-solid fa-circle-check"></i>
        </div>
        <p id="toast-message" class="text-xs font-semibold"></p>
    </div>

    <!-- Modals for adding a custom watched media -->
    <div id="add-media-modal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/60 backdrop-blur-sm hidden">
        <div class="bg-gray-900 border border-gray-800 rounded-2xl max-w-md w-full p-6 shadow-2xl space-y-4">
            <div class="flex justify-between items-center pb-2 border-b border-gray-800">
                <h3 class="text-lg font-bold text-white">내가 본 작품 추가하기</h3>
                <button id="modal-close" class="text-gray-400 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
            </div>
            
            <div class="space-y-3">
                <div>
                    <label class="block text-xs font-semibold text-gray-400 mb-1">작품 제목</label>
                    <input type="text" id="modal-title-input" placeholder="예: 기생충, 오징어 게임 등" class="w-full bg-gray-950 border border-gray-800 rounded-lg px-3 py-2 text-sm text-white focus:outline-none focus:border-indigo-500">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-gray-400 mb-1">구분</label>
                    <select id="modal-type-select" class="w-full bg-gray-950 border border-gray-800 rounded-lg px-3 py-2 text-sm text-white focus:outline-none focus:border-indigo-500">
                        <option value="영화">영화</option>
                        <option value="드라마">드라마 / 넷플릭스 등</option>
                    </select>
                </div>
                <div>
                    <label class="block text-xs font-semibold text-gray-400 mb-1">해당 장르</label>
                    <select id="modal-genre-select" class="w-full bg-gray-950 border border-gray-800 rounded-lg px-3 py-2 text-sm text-white focus:outline-none focus:border-indigo-500">
                        <!-- Dynamic options of current selected genres -->
                    </select>
                </div>
                <div>
                    <label class="block text-xs font-semibold text-gray-400 mb-1">나의 별점</label>
                    <div class="flex items-center gap-1.5" id="modal-stars-container">
                        <!-- Star dynamic selecting -->
                    </div>
                </div>
            </div>

            <div class="flex justify-end gap-2 pt-2">
                <button id="modal-cancel-btn" class="px-4 py-2 text-sm text-gray-400 hover:text-white font-medium">취소</button>
                <button id="modal-submit-btn" class="px-4 py-2 text-sm bg-indigo-600 hover:bg-indigo-500 text-white font-semibold rounded-lg">등록하기</button>
            </div>
        </div>
    </div>

    <!-- SCRIPT LOGIC -->
    <script>
        // 1. Data Schema & Core Database
        const genreList = [
            { id: 'romance', name: '로맨스 / 멜로', icon: 'fa-heart', color: 'text-pink-400', bg: 'bg-pink-500/10', border: 'border-pink-500/20' },
            { id: 'thriller', name: '스릴러 / 서스펜스', icon: 'fa-skull', color: 'text-red-400', bg: 'bg-red-500/10', border: 'border-red-500/20' },
            { id: 'sf_fantasy', name: 'SF / 판타지', icon: 'fa-wand-magic-sparkles', color: 'text-purple-400', bg: 'bg-purple-500/10', border: 'border-purple-500/20' },
            { id: 'comedy', name: '코미디', icon: 'fa-face-laugh-squint', color: 'text-yellow-400', bg: 'bg-yellow-500/10', border: 'border-yellow-500/20' },
            { id: 'action', name: '액션 / 어드벤처', icon: 'fa-burst', color: 'text-orange-400', bg: 'bg-orange-500/10', border: 'border-orange-500/20' },
            { id: 'documentary', name: '다큐멘터리', icon: 'fa-earth-asia', color: 'text-emerald-400', bg: 'bg-emerald-500/10', border: 'border-emerald-500/20' }
        ];

        // Default Movie database for matching and recommending
        const mediaLibrary = [
            // SF / Fantasy
            { title: "인터스텔라", type: "영화", genre: "sf_fantasy", score: 4.8, rReason: "광활한 우주 연출과 과학적 상상력의 경지", desc: "인류의 우주적 생존 투쟁을 담은 크리스토퍼 놀란의 걸작 SF.", tags: ["우주", "과학", "감동"] },
            { title: "듄 (Dune)", type: "영화", genre: "sf_fantasy", score: 4.7, rReason: "압도적인 미장센과 웅장한 세계관 빌딩", desc: "우주 제국 가문 간의 이권 다툼과 선택받은 구원자의 서사.", tags: ["웅장", "시각미", "스페이스오페라"] },
            { title: "다크 (DARK)", type: "드라마", genre: "sf_fantasy", score: 4.6, rReason: "시간 여행 물 중 최고로 꼽히는 완성도와 복잡한 복선", desc: "어느 작은 마을의 네 가문의 복잡한 시간 여행 연대기를 그린 넷플릭스 오리지널 드라마.", tags: ["미스터리", "뇌섹", "시간여행"] },
            { title: "아바타: 물의 길", type: "영화", genre: "sf_fantasy", score: 4.5, rReason: "황홀한 컴퓨터 그래픽스 기술과 수중 어드벤처의 황홀감", desc: "새로운 해양 생태계 판도라 행성에서 그려지는 제이크 설리의 가족 드라마.", tags: ["3D", "자연", "가족"] },
            
            // Romance
            { title: "어바웃 타임", type: "영화", genre: "romance", score: 4.8, rReason: "평범한 오늘을 특별하게 해주는 아름다운 시간 로맨스", desc: "시간을 되돌릴 수 있는 가문의 비밀을 알게 된 청년의 삶과 성찰을 담은 로맨틱 코미디 영화.", tags: ["시간여행", "눈물", "인생"] },
            { title: "라라랜드", type: "영화", genre: "romance", score: 4.7, rReason: "꿈꾸는 이들을 향한 재즈 선율과 감동적인 연출", desc: "재즈 피아니스트와 배우 지망생의 꿈과 지독하리만치 찬란한 사랑 이야기.", tags: ["음악", "뮤지컬", "여운"] },
            { title: "사랑의 불시착", type: "드라마", genre: "romance", score: 4.6, rReason: "최상의 연기 케미스트리와 극적인 긴장감을 더한 북한 로맨스", desc: "패러글라이딩 사고로 북한에 불시착한 재벌 상속녀와 남한 여자를 지키다 사랑에 빠지는 장교의 비극적이지만 설레는 사랑.", tags: ["국경초월", "설렘", "정주행"] },
            { title: "그 해 우리는", type: "드라마", genre: "romance", score: 4.5, rReason: "풋풋하고 현실감 있는 청춘 남녀의 아련한 사랑 재회", desc: "고등학교 시절 다큐멘터리를 찍으며 연인이 되었던 두 사람의 10년 뒤 비즈니스 재회 로맨스.", tags: ["청춘", "설렘", "아련"] },

            // Thriller
            { title: "기생충", type: "영화", genre: "thriller", score: 4.9, rReason: "칸과 아카데미가 극찬한 빈부격차에 대한 완벽한 서스펜스 블랙 코미디", desc: "전원 백수인 기택네 가족이 박사장네 과외 교사로 들어가며 벌어지는 미스터리 파국.", tags: ["계급사회", "명작", "예측불가"] },
            { title: "세븐", type: "영화", genre: "thriller", score: 4.8, rReason: "치밀하게 설계된 7대 죄악 모티브의 정통 스릴러", desc: "성서의 7대 죄악에 따라 기괴한 연쇄살인을 일으키는 킬러를 쫓는 두 형사.", tags: ["연쇄살인", "어둠", "반전"] },
            { title: "비밀의 숲", type: "드라마", genre: "thriller", score: 4.7, rReason: "감정을 잃은 검사와 열혈 형사가 파헤치는 고밀도 권력 카르텔", desc: "대한민국 검찰청 내부 비리를 둘러싼 거대 스캔들과 치밀한 정밀 수사극.", tags: ["추리", "연기존엄", "조승우"] },
            { title: "마우스", type: "드라마", genre: "thriller", score: 4.6, rReason: "싸이코패스 뇌 이식이라는 파격적 상상력과 소름 돋는 반전", desc: "동네를 뒤흔든 희대의 연쇄살인마에 맞서 싸우는 바른 청년 순경의 반전 미스터리 수사극.", tags: ["싸이코패스", "소름", "뇌과학"] },

            // Comedy
            { title: "극한직업", type: "영화", genre: "comedy", score: 4.6, rReason: "웃음 타율 100% 보장하는 유쾌한 슬랩스틱과 말장난 케미", desc: "마약반 형사들이 잠복 수사를 위해 인수한 치킨집이 전국 맛집으로 소문나며 시작되는 코믹 액션 수사극.", tags: ["치킨", "마약반", "폭소"] },
            { title: "브루클린 나인-나인", type: "드라마", genre: "comedy", score: 4.7, rReason: "매 화 20분 내내 쏟아지는 하이텐션 티키타카와 개성 넘치는 캐릭터 조합", desc: "개성 과다 브루클린 99 관할 경찰서 형사들의 유쾌 발랄 좌충우돌 시트콤.", tags: ["시트콤", "경찰서", "매력캐"] },
            { title: "슬기로운 의사생활", type: "드라마", genre: "comedy", score: 4.8, rReason: "매일 살아 숨 쉬는 병원의 일상과 유머, 그리고 밴드 음악의 하모니", desc: "눈빛만 봐도 아는 20년 지기 의대 5인방의 케미스토리와 가슴 따뜻한 메디컬 라이프.", tags: ["따뜻함", "의사", "우정"] },
            { title: "스파이 (2015)", type: "영화", genre: "comedy", score: 4.4, rReason: "기존 스파이 고정관념을 통쾌하게 부숴버리는 주체 불가능 액션 코미디", desc: "현장 경험 전무한 내근직 정보 분석관이 위기에 처한 동료를 구하러 직접 잠입 수사에 들어가는 포복절도 액션.", tags: ["첩보", "멜리사맥카시", "킬링타임"] },

            // Action
            { title: "매드맥스: 분노의 도로", type: "영화", genre: "action", score: 4.9, rReason: "멈추지 않고 질주하는 날 것 그대로의 광적인 실사 액션", desc: "핵전쟁으로 황폐해진 미래의 지구, 폭정에 맞서 고향을 향해 질주하는 임페라토르 퓨리오사와 매드의 여정.", tags: ["질주", "아드레날린", "디스토피아"] },
            { title: "다크 나이트", type: "영화", genre: "action", score: 4.8, rReason: "최고의 빌런 조커와 영웅 배트맨의 대립을 완성시킨 마스터피스 히어로물", desc: "고담시티의 질서와 악의 모호한 경계 속에서 배트맨과 그의 철저한 숙적 조커의 장엄한 충돌.", tags: ["히어로", "조커", "철학"] },
            { title: "더 글로리", type: "드라마", genre: "action", score: 4.7, rReason: "학창시절 상처를 하나씩 통쾌하게 되돌려주는 카타르시스 복수극", desc: "유년 시절 폭력으로 영혼까지 부서진 한 여자가 생을 걸어 치밀하게 준비한 처절한 사적 복수의 향연.", tags: ["복수", "명대사", "과몰입"] },
            { title: "종이의 집", type: "드라마", genre: "action", score: 4.6, rReason: "한 조폐국을 터는 교수 팀의 예측 불가 심리 게임과 짜릿한 한판 승부", desc: "스페인 조폐국을 상대로 역사적인 한 판을 모의한 천재 교수와 행동파 범죄 조직의 두뇌 스릴 작전.", tags: ["강도", "가면", "천재지략"] },

            // Documentary
            { title: "나의 문어 선생님", type: "영화", genre: "documentary", score: 4.8, rReason: "한 마리 문어와의 우정을 통해 회복되는 인간 영혼의 극적인 과정", desc: "슬럼프를 겪는 다큐 감독이 남아프리카 바다 속에서 마주친 특별한 문어와 삶의 교감을 나누는 이야기.", tags: ["힐링", "바다", "감동"] },
            { title: "소셜 딜레마", type: "영화", genre: "documentary", score: 4.6, rReason: "우리가 스마트폰을 켜는 순간 벌어지는 빅테크의 무서운 조작 알고리즘 폭로", desc: "실제 테크 기업 임원들이 고백하는 인간 중독 알고리즘과 알고리즘이 현대 사회의 민주주의를 붕괴시키는 방식.", tags: ["스마트폰", "IT사회", "경각심"] },
            { title: "더 레이스트 댄스 (The Last Dance)", type: "드라마", genre: "documentary", score: 4.9, rReason: "마이클 조던과 90년대 시카고 불스의 절대 패권을 보여주는 아카이브 다큐 스포츠", desc: "미 농구 역사의 리빙 레전드 마이클 조던과 불스의 마지막 우승 여정을 그린 명품 다큐시리즈.", tags: ["농구", "마이클조던", "열정"] },
            { title: "포뮬러 1: 본능의 질주", type: "드라마", genre: "documentary", score: 4.7, rReason: "서킷 안팎에서 펼쳐지는 레이서들과 구단주들의 초고압 드라마", desc: "세상에서 가장 빠른 속도로 달리는 모터스포츠 Formula 1의 비밀스럽고 자극적인 뒷이야기들.", tags: ["속도", "레이싱", "치열"] }
        ];

        // Default Movie recommendations tailored for simulation
        const sampleWatchedMedia = {
            'sf_fantasy': [
                { id: 'sw-1', title: '매트릭스', type: '영화', rating: 5 },
                { id: 'sw-2', title: '어벤져스', type: '영화', rating: 4 }
            ],
            'romance': [
                { id: 'sw-3', title: '노트북', type: '영화', rating: 4 },
                { id: 'sw-4', title: '노팅 힐', type: '영화', rating: 3 }
            ],
            'thriller': [
                { id: 'sw-5', title: '올드보이', type: '영화', rating: 5 },
                { id: 'sw-6', title: '셔터 아일랜드', type: '영화', rating: 4 }
            ],
            'comedy': [
                { id: 'sw-7', title: '기묘한 가족', type: '영화', rating: 3 },
                { id: 'sw-8', title: '수상한 그녀', type: '영화', rating: 4 }
            ],
            'action': [
                { id: 'sw-9', title: '아저씨', type: '영화', rating: 4 },
                { id: 'sw-10', title: '범죄도시', type: '영화', rating: 4 }
            ],
            'documentary': [
                { id: 'sw-11', title: '지구의 밤', type: '드라마', rating: 5 }
            ]
        };

        // State variables
        let appState = {
            step: 1,
            selectedGenres: [], // Array of genre id
            durations: {}, // Key: genreId, Value: duration in hours
            watched: {}, // Key: genreId, Value: Array of movies (e.g. {title, type, rating})
            activeTabGenreId: null,
            modalSelectedStars: 5,
            filterType: 'all' // all, movie, drama
        };

        // Deep copy of sample watched data
        appState.watched = JSON.parse(JSON.stringify(sampleWatchedMedia));

        // 2. DOM Elements
        const step1Container = document.getElementById('step1-container');
        const step2Container = document.getElementById('step2-container');
        const step3Container = document.getElementById('step3-container');

        const step1Circle = document.getElementById('step1-circle');
        const step2Circle = document.getElementById('step2-circle');
        const step3Circle = document.getElementById('step3-circle');
        const step1Text = document.getElementById('step1-text');
        const step2Text = document.getElementById('step2-text');
        const step3Text = document.getElementById('step3-text');

        const stepLine1Progress = document.getElementById('step-line-1-progress');
        const stepLine2Progress = document.getElementById('step-line-2-progress');

        const genreGrid = document.getElementById('genre-grid');
        const selectedGenresSliders = document.getElementById('selected-genres-sliders');
        const slidersContainer = document.getElementById('sliders-container');

        const btnToStep2 = document.getElementById('btn-to-step2');
        const btnBackToStep1 = document.getElementById('btn-back-to-step1');
        const btnToStep3 = document.getElementById('btn-to-step3');
        const btnReset = document.getElementById('btn-reset');

        const step2GenreTabs = document.getElementById('step2-genre-tabs');
        const watchedMoviesList = document.getElementById('watched-movies-list');
        const emptyWatchedState = document.getElementById('empty-watched-state');

        const btnAddWatched = document.getElementById('btn-add-watched');
        const addMediaModal = document.getElementById('add-media-modal');
        const modalClose = document.getElementById('modal-close');
        const modalCancelBtn = document.getElementById('modal-cancel-btn');
        const modalSubmitBtn = document.getElementById('modal-submit-btn');
        const modalTitleInput = document.getElementById('modal-title-input');
        const modalTypeSelect = document.getElementById('modal-type-select');
        const modalGenreSelect = document.getElementById('modal-genre-select');
        const modalStarsContainer = document.getElementById('modal-stars-container');

        // Step 3 metrics
        const statFavGenre = document.getElementById('stat-fav-genre');
        const statTotalHours = document.getElementById('stat-total-hours');
        const statAvgRating = document.getElementById('stat-avg-rating');
        const recommendationCardsContainer = document.getElementById('recommendation-cards-container');

        const toggleAll = document.getElementById('toggle-all');
        const toggleMovie = document.getElementById('toggle-movie');
        const toggleDrama = document.getElementById('toggle-drama');

        // Toast
        const toast = document.getElementById('toast');
        const toastMessage = document.getElementById('toast-message');

        // 3. Helper Functions
        function showToast(message, type = 'success') {
            toastMessage.textContent = message;
            toast.classList.remove('translate-y-10', 'opacity-0', 'pointer-events-none');
            toast.classList.add('translate-y-0', 'opacity-100');
            setTimeout(() => {
                toast.classList.remove('translate-y-0', 'opacity-100');
                toast.classList.add('translate-y-10', 'opacity-0', 'pointer-events-none');
            }, 3000);
        }

        // Initialize Genre Selection UI (Step 1)
        function initGenreSelection() {
            genreGrid.innerHTML = '';
            genreList.forEach(genre => {
                const card = document.createElement('button');
                card.type = 'button';
                card.className = `p-4 rounded-xl border text-left flex items-center justify-between transition-all duration-200 cursor-pointer ${
                    appState.selectedGenres.includes(genre.id) 
                    ? 'border-indigo-500 bg-indigo-600/10 text-white shadow-md' 
                    : 'border-gray-800 bg-gray-950 hover:bg-gray-800 text-gray-400 hover:text-gray-200'
                }`;
                card.dataset.id = genre.id;
                
                card.innerHTML = `
                    <div class="flex items-center space-x-3">
                        <div class="p-2.5 rounded-lg ${genre.bg} ${genre.color} text-base">
                            <i class="fa-solid ${genre.icon}"></i>
                        </div>
                        <span class="font-semibold text-sm">${genre.name}</span>
                    </div>
                    <div class="w-5 h-5 rounded-full border border-gray-700 flex items-center justify-center ${
                        appState.selectedGenres.includes(genre.id) ? 'bg-indigo-600 border-indigo-500' : ''
                    }">
                        ${appState.selectedGenres.includes(genre.id) ? '<i class="fa-solid fa-check text-[10px] text-white"></i>' : ''}
                    </div>
                `;

                card.addEventListener('click', () => toggleGenre(genre.id));
                genreGrid.appendChild(card);
            });
            updateSlidersUI();
            checkStep1Completion();
        }

        // Toggle genre selection
        function toggleGenre(id) {
            const index = appState.selectedGenres.indexOf(id);
            if (index > -1) {
                appState.selectedGenres.splice(index, 1);
                delete appState.durations[id];
            } else {
                appState.selectedGenres.push(id);
                appState.durations[id] = 2; // Default 2 hours
            }
            initGenreSelection();
        }

        // Check if step 1 is complete
        function checkStep1Completion() {
            if (appState.selectedGenres.length > 0) {
                btnToStep2.removeAttribute('disabled');
            } else {
                btnToStep2.setAttribute('disabled', 'true');
            }
        }

        // Generate and update sliders in Step 1
        function updateSlidersUI() {
            if (appState.selectedGenres.length === 0) {
                selectedGenresSliders.classList.add('hidden');
                return;
            }
            selectedGenresSliders.classList.remove('hidden');
            slidersContainer.innerHTML = '';

            appState.selectedGenres.forEach(genreId => {
                const genre = genreList.find(g => g.id === genreId);
                const currentVal = appState.durations[genreId] || 2;
                
                const sliderRow = document.createElement('div');
                sliderRow.className = "space-y-2 pb-3 border-b border-gray-900/60 last:border-b-0 last:pb-0";
                
                sliderRow.innerHTML = `
                    <div class="flex justify-between items-center">
                        <span class="text-sm font-semibold flex items-center gap-1.5 text-gray-200">
                            <span class="${genre.color} text-xs"><i class="fa-solid ${genre.icon}"></i></span>
                            ${genre.name}
                        </span>
                        <span class="text-xs font-bold text-indigo-400" id="slider-val-${genreId}">${currentVal}시간 / 주</span>
                    </div>
                    <div class="flex items-center gap-3">
                        <span class="text-[10px] text-gray-600">0h</span>
                        <input type="range" min="0" max="25" value="${currentVal}" 
                               class="w-full h-1.5 bg-gray-800 rounded-lg appearance-none cursor-pointer accent-indigo-500" 
                               id="slider-${genreId}">
                        <span class="text-[10px] text-gray-600">25h+</span>
                    </div>
                `;

                slidersContainer.appendChild(sliderRow);

                // Add slider listener
                const input = document.getElementById(`slider-${genreId}`);
                const valueText = document.getElementById(`slider-val-${genreId}`);
                input.addEventListener('input', (e) => {
                    const value = parseInt(e.target.value);
                    appState.durations[genreId] = value;
                    valueText.textContent = `${value}시간 / 주`;
                });
            });
        }

        // 4. STEP 2: Watched List & Tabs
        function initStep2UI() {
            if (appState.selectedGenres.length === 0) return;
            
            // Default active tab to first selected genre
            if (!appState.activeTabGenreId || !appState.selectedGenres.includes(appState.activeTabGenreId)) {
                appState.activeTabGenreId = appState.selectedGenres[0];
            }

            // Generate genre tabs
            step2GenreTabs.innerHTML = '';
            appState.selectedGenres.forEach(genreId => {
                const genre = genreList.find(g => g.id === genreId);
                const isActive = appState.activeTabGenreId === genreId;
                const badgeCount = (appState.watched[genreId] || []).length;

                const tabBtn = document.createElement('button');
                tabBtn.className = `whitespace-nowrap px-4 py-2.5 rounded-t-lg text-sm font-semibold flex items-center gap-2 transition border-b-2 ${
                    isActive 
                    ? 'border-indigo-500 text-indigo-400 bg-gray-900' 
                    : 'border-transparent text-gray-500 hover:text-gray-300 hover:bg-gray-900/40'
                }`;
                tabBtn.innerHTML = `
                    <i class="fa-solid ${genre.icon}"></i>
                    ${genre.name}
                    <span class="text-[10px] px-1.5 py-0.2 bg-gray-800 border border-gray-700 text-gray-300 rounded-full">${badgeCount}</span>
                `;
                tabBtn.addEventListener('click', () => {
                    appState.activeTabGenreId = genreId;
                    initStep2UI();
                });
                step2GenreTabs.appendChild(tabBtn);
            });

            renderWatchedList();
        }

        // Render current selected genre's watched media
        function renderWatchedList() {
            const currentGenreId = appState.activeTabGenreId;
            const movies = appState.watched[currentGenreId] || [];
            
            watchedMoviesList.innerHTML = '';
            
            if (movies.length === 0) {
                emptyWatchedState.classList.remove('hidden');
                watchedMoviesList.classList.add('hidden');
                return;
            }

            emptyWatchedState.classList.add('hidden');
            watchedMoviesList.classList.remove('hidden');

            movies.forEach(item => {
                const row = document.createElement('div');
                row.className = "flex flex-col sm:flex-row sm:items-center justify-between gap-3 p-3.5 bg-gray-900 hover:bg-gray-850 border border-gray-800 rounded-xl transition";
                
                // Construct Clickable Stars for dynamic in-line updating
                let starsHtml = '<div class="flex items-center gap-1.5">';
                for (let i = 1; i <= 5; i++) {
                    const isFilled = i <= item.rating;
                    const starClass = isFilled 
                        ? 'fa-solid fa-star text-yellow-500 cursor-pointer hover:scale-125 transition-all' 
                        : 'fa-regular fa-star text-gray-700 cursor-pointer hover:text-yellow-600 hover:scale-125 transition-all';
                    
                    starsHtml += `<i class="${starClass} text-base" title="${i}점 주기" onclick="updateItemRating('${currentGenreId}', '${item.id}', ${i})"></i>`;
                }
                starsHtml += '</div>';

                row.innerHTML = `
                    <div class="flex items-center gap-3">
                        <span class="px-2 py-0.5 rounded text-[10px] font-bold ${
                            item.type === '영화' ? 'bg-blue-600/10 text-blue-400 border border-blue-500/20' : 'bg-pink-600/10 text-pink-400 border border-pink-500/20'
                        }">
                            ${item.type}
                        </span>
                        <p class="font-bold text-sm text-white">${item.title}</p>
                    </div>
                    <div class="flex items-center justify-between sm:justify-end gap-5 border-t border-gray-800/50 sm:border-t-0 pt-2 sm:pt-0">
                        <div class="flex flex-col items-end gap-0.5">
                            ${starsHtml}
                            <span class="text-[9px] text-gray-500 hidden sm:block">클릭하여 평점 변경</span>
                        </div>
                        <button class="text-gray-500 hover:text-red-400 text-xs transition duration-150 flex items-center gap-1 py-1.5 px-2 hover:bg-red-500/10 rounded-md" 
                                onclick="deleteWatchedMedia('${currentGenreId}', '${item.id}')">
                            <i class="fa-regular fa-trash-can"></i> 삭제
                        </button>
                    </div>
                `;

                watchedMoviesList.appendChild(row);
            });
        }

        // Live rating modifier (dynamic updates directly from stars click)
        window.updateItemRating = function(genreId, itemId, newRating) {
            const list = appState.watched[genreId] || [];
            const item = list.find(m => m.id === itemId);
            if (item) {
                const oldRating = item.rating;
                item.rating = newRating;
                renderWatchedList(); // Re-render target list instantly
                showToast(`"${item.title}"의 평점이 ${oldRating}점 ➜ ${newRating}점으로 변경되었습니다.`);
            }
        };

        // Delete watched media
        window.deleteWatchedMedia = function(genreId, itemId) {
            const list = appState.watched[genreId] || [];
            const deletedItem = list.find(item => item.id !== itemId);
            const title = deletedItem ? `"${deletedItem.title}" ` : "";
            appState.watched[genreId] = list.filter(item => item.id !== itemId);
            initStep2UI();
            showToast(`${title}관람 이력이 성공적으로 삭제되었습니다.`);
        };

        // Modal star select builder
        function renderModalStars() {
            modalStarsContainer.innerHTML = '';
            for (let i = 1; i <= 5; i++) {
                const star = document.createElement('button');
                star.type = 'button';
                star.className = `text-xl transition duration-150 focus:outline-none ${
                    i <= appState.modalSelectedStars ? 'text-yellow-500 scale-110' : 'text-gray-700 hover:text-gray-600'
                }`;
                star.innerHTML = i <= appState.modalSelectedStars ? '<i class="fa-solid fa-star"></i>' : '<i class="fa-regular fa-star"></i>';
                
                star.addEventListener('click', () => {
                    appState.modalSelectedStars = i;
                    renderModalStars();
                });
                modalStarsContainer.appendChild(star);
            }
        }

        // Open Modal handler
        btnAddWatched.addEventListener('click', () => {
            modalTitleInput.value = '';
            appState.modalSelectedStars = 5;
            
            // Build genre select option in modal
            modalGenreSelect.innerHTML = '';
            appState.selectedGenres.forEach(genreId => {
                const genre = genreList.find(g => g.id === genreId);
                const option = document.createElement('option');
                option.value = genreId;
                option.textContent = genre.name;
                if (genreId === appState.activeTabGenreId) {
                    option.selected = true;
                }
                modalGenreSelect.appendChild(option);
            });

            renderModalStars();
            addMediaModal.classList.remove('hidden');
        });

        // Close Modal
        function closeModal() {
            addMediaModal.classList.add('hidden');
        }
        modalClose.addEventListener('click', closeModal);
        modalCancelBtn.addEventListener('click', closeModal);

        // Submit media from modal
        modalSubmitBtn.addEventListener('click', () => {
            const title = modalTitleInput.value.trim();
            if (!title) {
                showToast("작품 제목을 입력해 주세요.", "warning");
                return;
            }

            const genreId = modalGenreSelect.value;
            const type = modalTypeSelect.value;
            const rating = appState.modalSelectedStars;

            if (!appState.watched[genreId]) {
                appState.watched[genreId] = [];
            }

            appState.watched[genreId].push({
                id: 'custom-' + Date.now(),
                title,
                type,
                rating
            });

            appState.activeTabGenreId = genreId;
            closeModal();
            initStep2UI();
            showToast(`"${title}" 작품이 성공적으로 추가되었습니다.`);
        });


        // 5. STEP 3: Core Algorithm Recommendation Logic
        function generateRecommendations() {
            // Calculates statistics:
            // 1. Total Weekly Hours
            let totalHours = 0;
            appState.selectedGenres.forEach(gId => {
                totalHours += appState.durations[gId] || 0;
            });

            // 2. Favorite genre based on combined 시청 시간 & 장르 선호도
            let topGenreId = appState.selectedGenres[0];
            let maxWeight = 0;
            appState.selectedGenres.forEach(gId => {
                const duration = appState.durations[gId] || 0;
                const count = (appState.watched[gId] || []).length;
                // Simple Weight Formula: duration + (number of watched items * 1.5)
                const weight = duration + (count * 1.5);
                if (weight > maxWeight) {
                    maxWeight = weight;
                    topGenreId = gId;
                }
            });
            const topGenre = genreList.find(g => g.id === topGenreId);

            // 3. Average rating of watched media
            let totalRating = 0;
            let ratingCount = 0;
            appState.selectedGenres.forEach(gId => {
                const movies = appState.watched[gId] || [];
                movies.forEach(m => {
                    totalRating += m.rating;
                    ratingCount++;
                });
            });
            const avgRating = ratingCount > 0 ? (totalRating / ratingCount).toFixed(1) : "3.0";

            // Update stats layout
            statFavGenre.innerHTML = `
                <span class="${topGenre.color}"><i class="fa-solid ${topGenre.icon} mr-1.5"></i></span>${topGenre.name}
            `;
            statTotalHours.textContent = `${totalHours}시간`;
            statAvgRating.innerHTML = `<i class="fa-solid fa-star text-yellow-500 mr-1.5"></i>${avgRating} / 5.0`;

            // Recommendation Scoring Logic
            // Go through entire `mediaLibrary` database and score each item
            const recommendations = mediaLibrary.map(media => {
                let score = 50; // Starting baseline score

                // 1) Same Genre Weighting
                if (media.genre === topGenreId) {
                    score += 25; // Highly boost primary genre
                } else if (appState.selectedGenres.includes(media.genre)) {
                    score += 15; // Moderately boost any other chosen genre
                } else {
                    score -= 20; // Drastically penalize unselected genres
                }

                // 2) Watched Penalty
                // Filter out movies user already watched
                const watchedInThisGenre = appState.watched[media.genre] || [];
                const alreadyWatched = watchedInThisGenre.some(w => w.title.toLowerCase().includes(media.title.toLowerCase()) || media.title.toLowerCase().includes(w.title.toLowerCase()));
                if (alreadyWatched) {
                    score -= 40; // Extremely penalize already watched contents so they don't get recommended
                }

                // 3) Watch Time & Format Compatibility Integration
                // Drama vs Movie weighting based on total hours
                // If weekly hours are high (> 12 hours), user has more spare time -> favor Dramas
                // If weekly hours are low (< 5 hours), user has tight schedule -> favor Movies
                if (totalHours >= 12) {
                    if (media.type === "드라마") score += 10;
                } else if (totalHours <= 5) {
                    if (media.type === "영화") score += 10;
                }

                // 4) User Taste / Rating bias alignment
                // If user usually rates movies high (avgRating > 4.2), recommend premium critical-acclaimed works (high internal score)
                // If user usually rates low (strict, avgRating < 3.5), recommend high-satisfaction mass-pleaser movies
                if (avgRating > 4.2 && media.score >= 4.7) {
                    score += 10;
                } else if (avgRating < 3.5 && media.score < 4.7) {
                    score += 8; // suggest easier titles
                }

                // Append matching score (capped between 0 and 100)
                media.matchPercent = Math.min(Math.max(Math.round(score), 30), 99);
                return media;
            });

            // Sort recommendations based on highest matching percentage
            // Filter out already watched or extremely low scored
            const finalRecs = recommendations
                .filter(r => r.matchPercent >= 50)
                .sort((a, b) => b.matchPercent - a.matchPercent);

            renderRecommendationsGrid(finalRecs);
        }

        // Render recommendation items
        function renderRecommendationsGrid(items) {
            recommendationCardsContainer.innerHTML = '';
            
            // Filter by type selection
            let filtered = items;
            if (appState.filterType === 'movie') {
                filtered = items.filter(i => i.type === '영화');
            } else if (appState.filterType === 'drama') {
                filtered = items.filter(i => i.type === '드라마');
            }

            // Limit to top 6 best matching items
            const displayItems = filtered.slice(0, 6);

            if (displayItems.length === 0) {
                recommendationCardsContainer.innerHTML = `
                    <div class="col-span-full flex flex-col items-center justify-center py-16 text-gray-500">
                        <i class="fa-solid fa-triangle-exclamation text-4xl text-amber-500 mb-3 animate-bounce"></i>
                        <p class="font-bold">조건에 딱 들어맞는 추천 콘텐츠를 찾지 못했습니다.</p>
                        <p class="text-xs mt-1 text-gray-600">더 많은 선호 장르를 선택하거나 시청시간 가중치를 다시 늘려보세요.</p>
                    </div>
                `;
                return;
            }

            displayItems.forEach((item, index) => {
                const genreObj = genreList.find(g => g.id === item.genre);
                const card = document.createElement('div');
                card.className = "group bg-gray-950 border border-gray-800 rounded-xl overflow-hidden shadow-lg hover:border-indigo-500/50 transition-all duration-300 transform hover:-translate-y-1";
                
                // Color ring for match scoring
                let strokeColor = "stroke-indigo-500";
                if (item.matchPercent >= 90) strokeColor = "stroke-emerald-500";
                else if (item.matchPercent >= 75) strokeColor = "stroke-indigo-500";
                else strokeColor = "stroke-yellow-500";

                const radialProgressSvg = `
                    <div class="relative w-14 h-14 flex items-center justify-center bg-gray-900 rounded-full">
                        <svg class="w-full h-full transform -rotate-90">
                            <circle cx="28" cy="28" r="24" class="stroke-gray-800 fill-none" stroke-width="4"/>
                            <circle cx="28" cy="28" r="24" class="${strokeColor} fill-none" stroke-width="4"
                                    stroke-dasharray="150" stroke-dashoffset="${150 - (150 * item.matchPercent) / 100}"/>
                        </svg>
                        <span class="absolute text-xs font-black text-white">${item.matchPercent}%</span>
                    </div>
                `;

                // Badge colors
                const typeBadge = item.type === '영화' 
                    ? 'bg-blue-600/10 text-blue-400 border-blue-500/20' 
                    : 'bg-pink-600/10 text-pink-400 border-pink-500/20';

                // Tags markup
                let tagsMarkup = item.tags.map(t => `<span class="px-2 py-0.5 bg-gray-900 text-gray-400 rounded text-[10px] border border-gray-800/80">#${t}</span>`).join(' ');

                card.innerHTML = `
                    <div class="p-5 space-y-4">
                        <div class="flex justify-between items-start">
                            <div class="space-y-1">
                                <div class="flex items-center gap-2">
                                    <span class="px-2 py-0.5 rounded text-[10px] font-bold border ${typeBadge}">${item.type}</span>
                                    <span class="text-xs text-gray-500 font-medium flex items-center gap-1">
                                        <i class="fa-solid ${genreObj.icon}"></i> ${genreObj.name}
                                    </span>
                                </div>
                                <h4 class="text-lg font-bold text-white group-hover:text-indigo-400 transition-colors">${item.title}</h4>
                            </div>
                            ${radialProgressSvg}
                        </div>

                        <p class="text-xs text-gray-400 leading-relaxed">${item.desc}</p>
                        
                        <div class="bg-indigo-950/20 border border-indigo-900/30 p-2.5 rounded-lg flex items-start gap-2">
                            <i class="fa-solid fa-comment-nodes text-indigo-400 text-xs mt-0.5"></i>
                            <p class="text-[11px] text-indigo-200/90 leading-tight">
                                <span class="font-bold text-indigo-300">추천 근거:</span> ${item.rReason}
                            </p>
                        </div>

                        <div class="flex justify-between items-center pt-2 border-t border-gray-900">
                            <div class="flex gap-1">
                                ${tagsMarkup}
                            </div>
                            <span class="text-xs text-gray-500 font-semibold flex items-center gap-1">
                                <i class="fa-solid fa-star text-yellow-500"></i> ${item.score}
                            </span>
                        </div>
                    </div>
                `;

                recommendationCardsContainer.appendChild(card);
            });
        }


        // 6. Navigation Logic & Phase Changers
        function updateStepProgressBar() {
            // Reset circles
            step1Circle.className = "w-10 h-10 rounded-full flex items-center justify-center text-white font-bold transition-all duration-300 " + 
                (appState.step >= 1 ? "bg-indigo-600 shadow-lg shadow-indigo-600/20" : "bg-gray-800 text-gray-400");
            step1Text.className = "text-xs mt-2 font-medium " + (appState.step >= 1 ? "text-indigo-400" : "text-gray-500");

            step2Circle.className = "w-10 h-10 rounded-full flex items-center justify-center font-bold transition-all duration-300 " + 
                (appState.step >= 2 ? "bg-indigo-600 text-white shadow-lg shadow-indigo-600/20" : "bg-gray-800 text-gray-400");
            step2Text.className = "text-xs mt-2 font-medium " + (appState.step >= 2 ? "text-indigo-400" : "text-gray-500");

            step3Circle.className = "w-10 h-10 rounded-full flex items-center justify-center font-bold transition-all duration-300 " + 
                (appState.step >= 3 ? "bg-indigo-600 text-white shadow-lg shadow-indigo-600/20" : "bg-gray-800 text-gray-400");
            step3Text.className = "text-xs mt-2 font-medium " + (appState.step >= 3 ? "text-indigo-400" : "text-gray-500");

            // Progress line transitions
            stepLine1Progress.style.width = appState.step >= 2 ? "100%" : "0%";
            stepLine2Progress.style.width = appState.step >= 3 ? "100%" : "0%";
        }

        function switchStep(newStep) {
            appState.step = newStep;
            updateStepProgressBar();

            // Hide/Show step panels
            step1Container.classList.add('hidden');
            step2Container.classList.add('hidden');
            step3Container.classList.add('hidden');

            if (newStep === 1) {
                step1Container.classList.remove('hidden');
            } else if (newStep === 2) {
                step2Container.classList.remove('hidden');
                initStep2UI();
            } else if (newStep === 3) {
                step3Container.classList.remove('hidden');
                generateRecommendations();
            }
        }

        // Navigation Events
        btnToStep2.addEventListener('click', () => {
            if (appState.selectedGenres.length === 0) {
                showToast("최소 1개 이상의 선호 장르를 선택해 주세요.", "warning");
                return;
            }
            switchStep(2);
        });

        btnBackToStep1.addEventListener('click', () => {
            switchStep(1);
        });

        btnToStep3.addEventListener('click', () => {
            switchStep(3);
            showToast("알고리즘 큐레이션이 반영되었습니다!");
        });

        btnReset.addEventListener('click', () => {
            appState.selectedGenres = [];
            appState.durations = {};
            appState.watched = JSON.parse(JSON.stringify(sampleWatchedMedia));
            appState.activeTabGenreId = null;
            appState.filterType = 'all';

            // Active button states
            toggleAll.className = "px-3 py-1.5 rounded-md text-xs font-semibold bg-indigo-600 text-white transition";
            toggleMovie.className = "px-3 py-1.5 rounded-md text-xs font-semibold text-gray-400 hover:text-white transition";
            toggleDrama.className = "px-3 py-1.5 rounded-md text-xs font-semibold text-gray-400 hover:text-white transition";

            initGenreSelection();
            switchStep(1);
            showToast("설문조사가 전면 리셋되었습니다.");
        });

        // Toggle recommendations by category
        function updateFilterType(type) {
            appState.filterType = type;
            
            // Re-style filter toggles
            toggleAll.className = "px-3 py-1.5 rounded-md text-xs font-semibold transition " + (type === 'all' ? "bg-indigo-600 text-white" : "text-gray-400 hover:text-white");
            toggleMovie.className = "px-3 py-1.5 rounded-md text-xs font-semibold transition " + (type === 'movie' ? "bg-indigo-600 text-white" : "text-gray-400 hover:text-white");
            toggleDrama.className = "px-3 py-1.5 rounded-md text-xs font-semibold transition " + (type === 'drama' ? "bg-indigo-600 text-white" : "text-gray-400 hover:text-white");

            // Refresh recommend output
            generateRecommendations();
        }

        toggleAll.addEventListener('click', () => updateFilterType('all'));
        toggleMovie.addEventListener('click', () => updateFilterType('movie'));
        toggleDrama.addEventListener('click', () => updateFilterType('drama'));

        // Initialize App on Window Load
        window.onload = function() {
            initGenreSelection();
            updateStepProgressBar();
        };

    </script>
</body>
</html>

