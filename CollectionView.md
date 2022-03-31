# CollectionView

# CollectionViewLayout.invalidateLayout vs .reloadData()
  - Layout만 업데이트 vs Data 변경 및 Layout 업데이트
  - invalidateLayout은 레이아웃 객체에게 아이템이 지워지거나, 추가 되거나, 이동할때 필연적으로 자체 모든 레이아웃 속성을 재연산 하도록 합니다.
  
# UICollectionViewCompositionalLayout ( iOS 13+ )
  - FlexLayout와 유사하게 레이아웃을 설정할 수 있을 것 같다.
  - CollectionViewLayout을 유연하게 커스터마이징 할 수 있게해주는 클래스
    
  필수 구현 Object 
  
    - NSCollectionLayoutSize return NSCollectionLayoutSize(widthDimension: .absolute(100), heightDimension: .fractionalHeight(0.2))
      absolute = 고정 크기
      fractional = 속한 그룹의 크기에 대한 비율
      
    - NSCollectionLayoutItem 지정된 사이즈의 아이템
    
    - NSCollectionLayoutGroup 아이템들을 담고있는 그룹
    
    - NSCollectionLayoutSection 그룹을 담고있는 섹션
    
      section.orthogonalScrollingBehavior 스크롤 형식을 설정할 프로퍼티
      
      
        continuous - 일반적 이동가능

        continuousGroupLeadingBoundary - 무조건 전페이지의 leading으로이동

        groupPaging - 가까운 그룹으로 페이징효과(leading에 맞춰짐)

        groupPagingCentered - 그룹의 센터로 이동

        none - 스크롤 x

        paging - 컬렉션뷰기준 페이징
        
      
      
  선택적 구현 Object
  
    - NSCollectionLayoutSupplementaryItem
      NSCollectionLayoutSupplementaryItem(layoutSize: badgeSize, elementKind: "badge", containerAnchor: badgeAnchor)
      뱃지나 시각적 프레임 등으로 아이템에 표현될 객체
      UICollectionReusableView 클래스 생성하고 CollectionView에 등록 후 사용한다.
        
     
    - NSCollectionLayoutBoundarySupplementaryItem
      : 헤더뷰 혹은 푸터뷰의 레이아웃을 추가할 때 사용하는 객체
        사용법은 SupplementaryItem과 같다
        
    
        
