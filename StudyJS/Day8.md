#### 페이지 리프레시 안 되는 현상 
+ 홈 > 리스트 페이지 > 카테고리 선택 > 이전(홈) > 리스트 페이지 시, 이 전에 선택했던 카테고리의 상품만 노출된다.
+ 즉, 카테고리 리스트가 리셋이 안 된다.
+ 과연 아래 코드 중에 어떤 것이 리프레시를 해주는 역할을 할까❓❓
  + 바로 `this.ctgrSeqNo = 0` 코드이다.
  + 이 코드는 카테고리의 기본 시퀀스 번호를 '0'으로 지정하여 리스트가 조회될 때 카테고리가 '전체' 리스트를 조회하게 만든다.
  + 이 코드가 `ionViewWillEnter()`함수 안에 지정해준 이유는 이 페이지를 탈때마다 화면에 '전체' 리스트가 보이기 하기 위해서이다.
  + `ionViewWillEnter()`함수는 페이지를 탈 때마다 화면에 표시해주는 기능을 한다.
```node
data() {
  return {
    productList: [],
    selectedCategory: {
      key: '0', value: this.$t('all')
    },
    selectedSortingNm: this.$t('sortRegist'),
    categoryList: [],
    orderGbn: 'REG',
    ctgrSeqNo: 0,
    dlNo: 0,
  }
},
created() {
},
ionViewWillEnter() {
  this.orderGbn = 'REG'
  this.selectedCategory = {
    key: '0', value: this.$t('all')
  }
  this.ctgrSeqNo = 0

  this.dlNo = this.$route.params.dlNo
  this.resetCate()
  this.getStoreCategory()
  this.getList(this.ctgrSeqNo, this.orderGbn, this.dlNo)
},
methods: {
  // 카테고리 리스트 리셋
  resetCate() {
    this.categoryList = []
  },
  // 카페고리 조회
  async getStoreCategory() {
    const res = await getStoreCtgr('CT')
    const categories = res.data.categories
    this.categoryList.push({
      key: 0,
      value: this.$t('all')
    })
    for (let i = 0; i < categories.length; i++) {
      this.categoryList.push({
        key: categories[i].ctgrSeqNo,
        value: categories[i].ctgrNm
      })
    }
  },
  // 투어패스 리스트 조회
  getList(ctgrSeqNo, orderGbn, dlNo) { // 조회 순서(REG, RV, SAL, HP,LP)
    this.showLoading()
    this.productList = []
    const ctgrSeqNumber = ctgrSeqNo || null
    requstTourPassList({ ctgrSeqNo: ctgrSeqNumber, orderGbn, dlNo, page: 1, size: 100 }).then(res => {
      res.data.products.forEach(product => {
        this.productList.push({
          dlNo: product.dlNo,
          stORCtgr: product.ctgrNm,
          mainTitle: product.dlNm, // 상품 이름
          img: product.tmnlImgUrl, // 이미지
          originPrice: product.nmlAmt, // 상품가격(정상가)
          salesPrice: product.salAmt, // 판매가격
          fvrYn: product.fvrYn, // 즐겨찾기 여부
          fvrGbn: 'T', // 즐겨찾기 대상구분,
          fvrVal: product.dlNo, // 즐겨찾기 대상 번호
          rating: product.rvScr, // 별점
          rvCnt: product.rvCnt, // 리뷰 갯수
          DcYn: product.dcYn, // 할인 여부
          DcVal: product.dcVal, // 할인률?
          tags: product.tags
        })
      })
      this.dismissLoading()
    }).catch(err => {
      this.dismissLoading()
      console.log(err)
    })
  },
  selectCategory(ctgr) {
    this.ctgrSeqNo = ctgr.key
    this.selectedCategory = ctgr
    this.getList(this.ctgrSeqNo, this.orderGbn)
  },
}
```
