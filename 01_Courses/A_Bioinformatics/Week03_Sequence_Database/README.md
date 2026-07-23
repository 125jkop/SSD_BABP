# Week 3: 정보로서 다뤄지는 Sequence

본 3주차 활동에서는 지난 활동에서 알아본 데이터 분석 과정 중에서도 생물학적 데이터를 생성하고 확보하는 **수집(Collection)** 단계에 집중해봅니다.

생물학적 데이터가 어떻게 만들어지는지 DNA sequencing 기술의 발전 과정을 통해 알아보고, 수집한 데이터가 어떤 형식으로 저장되며 어디에서 찾아볼 수 있는지 살펴봅니다.

마찬가지로 텍스트 외에 pdf 파일과 ipynb 파일을 함께 업로드하였으니, 함께 보시면서 복습하시는 것을 추천드립니다.

---

## 생물 데이터의 수집

지난 활동에서는 데이터 분석의 과정을 크게 수집(Collection), 처리(Processing), 분석(Analysis)의 세 단계로 구분했습니다.

기상자료개방포털에서 날씨 데이터를 가져오고, 필요한 정보를 추출하여 가공한 뒤, 그래프로 시각화하고 해석하는 과정까지 함께 진행했습니다. 이번 활동에서는 이 중에서도 분석의 시작점이 되는 **데이터의 수집**에 집중합니다.

생명과학에서는 연구자가 직접 실험을 수행하여 데이터를 생산하기도 하지만, 이미 다른 연구자들이 생산하여 데이터베이스에 저장한 데이터를 가져와 분석하기도 합니다. 이번 주차에는 DNA의 염기서열을 읽어내는 DNA sequencing과, 그렇게 수집된 생물학적 정보를 찾아볼 수 있는 데이터베이스를 알아보았습니다.

## DNA Sequencing

DNA sequencing은 DNA를 구성하는 염기들이 어떤 순서로 배열되어 있는지 읽어내는 기술입니다.

초기의 대표적인 DNA sequencing 기술인 **Sanger sequencing**에서는 DNA 합성 과정에 사슬의 연장을 중단시키는 ddNTP를 사용합니다. 서로 다른 길이로 합성된 DNA 조각들을 크기에 따라 분리하고, 각 염기에 부착된 형광 신호를 감지하여 염기서열을 읽을 수 있습니다.

하지만 Sanger sequencing으로 한 번에 읽을 수 있는 서열의 길이에는 한계가 있습니다. 따라서 인간처럼 매우 긴 유전체를 분석하기 위해서는 DNA를 여러 조각으로 나누어 읽은 뒤, 다시 원래 순서대로 조립하는 과정이 필요합니다.

### Human Genome Project

Human Genome Project(HGP)는 인간의 염색체에 존재하는 전체 염기서열을 밝히기 위해 진행된 대규모 연구 프로젝트입니다.

공개 Human Genome Project에서는 Sanger sequencing을 기반으로 한 **Hierarchical shotgun sequencing** 방법이 사용되었습니다.

1. 유전체를 큰 조각으로 나누어 BAC(Bacterial Artificial Chromosome)에 삽입합니다.
2. STS(Sequence Tagged Site)를 이용해 각 DNA 조각의 상대적 위치를 나타내는 물리적 지도(Physical Map)를 작성합니다.
3. 지도에 배치된 DNA 조각을 다시 작게 파쇄하여 sequencing합니다.
4. 미리 작성한 물리적 지도를 바탕으로 짧게 읽은 서열들을 조립합니다.

HGP는 인간의 생리적 기전을 이해하기 위한 기반을 제공했으며, 유전자에서 나타나는 변화를 바탕으로 표현형을 연구하는 Reverse genetics와 개인의 유전적 특성을 고려하는 정밀 의료의 발전에도 기여했습니다.

다만 초기 인간 유전체 데이터는 일부 집단의 유전적 정보에 편향되어 있었으며, 당시 기술로는 centromere와 telomere처럼 반복 서열이 많은 영역을 정확하게 조립하기 어려웠다는 한계도 있었습니다.

## Next Generation Sequencing

기존 DNA sequencing은 많은 시간과 비용을 요구했으며, 한 번에 처리할 수 있는 데이터의 양에도 한계가 있었습니다.

이를 극복하기 위해 다수의 DNA 조각을 동시에 읽거나, 훨씬 긴 DNA 서열을 한 번에 읽을 수 있는 새로운 sequencing 기술들이 개발되었습니다. 이번 활동에서는 그중 Illumina, PacBio HiFi, Oxford Nanopore의 원리를 간단하게 살펴보았습니다.

* **Illumina**
  * 짧은 DNA 조각에 adapter와 index sequence를 부착합니다.
  * DNA 조각을 flow cell에 결합시킨 뒤 Bridge amplification을 통해 같은 서열의 cluster를 만듭니다.
  * DNA가 합성될 때 나타나는 형광 신호를 감지하여 염기서열을 읽습니다.
  * 한 번에 매우 많은 수의 짧은 서열을 읽을 수 있다는 특징이 있습니다.

* **PacBio HiFi sequencing**
  * 긴 DNA 조각의 양 끝에 adapter를 부착하여 원형의 DNA를 만듭니다.
  * DNA polymerase가 같은 DNA 조각을 반복해서 읽으며 실시간으로 형광 신호를 감지합니다.
  * 같은 서열을 여러 번 읽은 결과를 종합하여 길고 정확도가 높은 서열을 얻습니다.

* **Oxford Nanopore Technology**
  * Membrane에 만들어진 매우 작은 nanopore로 DNA를 통과시킵니다.
  * DNA가 pore를 통과할 때 발생하는 전류의 변화를 측정하여 염기서열을 읽습니다.
  * 매우 긴 DNA를 직접 읽을 수 있으며, 비교적 작은 장비로도 실시간 sequencing이 가능합니다.

각 기술의 자세한 작동 원리가 궁금하다면 아래 영상을 참고해주세요.

* [Illumina sequencing](https://www.youtube.com/watch?v=fCd6B5HRaZ8)
* [PacBio HiFi sequencing](https://www.youtube.com/watch?v=_lD8JyAbwEo)
* [Oxford Nanopore sequencing](https://www.youtube.com/watch?v=bS3NiFLwPqE)

---

## 생물정보학 데이터베이스: NCBI

Sequencing을 통해 많은 생물학적 데이터가 생산되더라도, 연구자 개인의 컴퓨터에만 저장되어 있다면 다른 연구자가 이를 활용하기 어렵습니다.

따라서 생산된 생물 데이터는 일정한 형식으로 정리되어 공공 데이터베이스에 등록됩니다. 대표적인 생물정보학 데이터베이스인 **NCBI(National Center for Biotechnology Information)**는 미국 국립보건원 산하에서 운영되며, 생명과학 연구에 필요한 여러 종류의 데이터와 분석 도구를 제공합니다.

NCBI에서는 목적에 따라 서로 다른 데이터베이스를 이용할 수 있습니다.

* **Gene**: 유전자와 관련된 서열, 위치, 기능 등의 정보를 제공합니다.
* **Protein**: 단백질의 아미노산 서열과 관련 정보를 제공합니다.
* **SNP**: 생물에서 발견된 단일염기다형성 등의 유전적 변이 정보를 제공합니다.
* **PubChem**: 유기 물질과 화합물의 구조 및 생화학적 정보를 제공합니다.
* **PubMed**: 생명과학과 의학 분야의 학술 문헌을 검색할 수 있습니다.

또한 NCBI의 **BLAST(Basic Local Alignment Search Tool)**를 이용하면 자신이 가진 DNA 또는 단백질 서열을 데이터베이스의 다른 서열과 비교하여 유사한 서열을 찾아볼 수 있습니다.

각 데이터베이스에 직접 접속하여 자신이 알고 있는 유전자, 단백질, 변이, 화합물 또는 논문을 한 번씩 검색해보시길 바랍니다.

## FASTQ와 FASTA

Sequencing으로 생성된 염기서열 데이터는 목적에 맞는 파일 형식으로 저장해야 합니다.

- **FASTQ**
sequencing을 통해 읽은 염기서열과 각 염기의 sequencing quality를 함께 저장하는 형식입니다. 따라서 sequencing 직후의 데이터가 얼마나 신뢰할 수 있는지를 확인하고, 품질이 낮은 부분을 제거하는 전처리 과정에 활용할 수 있습니다.

- **FASTA**
서열 자체를 저장하거나 분석에 활용하기 위해 널리 사용되는 비교적 구조가 단순한 형식입니다.

FASTA 파일은 크게 두 부분으로 구성됩니다.

* `>`로 시작하는 첫 번째 줄에는 서열의 이름과 설명 등 metadata가 기록
* 그 아래 줄부터는 실제 DNA, RNA 또는 단백질의 sequence가 기록

## 데이터의 준비
**GFP(Green fluorescent protein)**는 내부의 chromophore를 β-barrel 구조가 둘러싸고 있는 단백질로, 살아있는 세포에서 타겟 단백질의 유전자에 융합시켜 발현되는 양상을 형광 신호로 추적하는 등 생명과학 연구에서 자주 사용되는 단백질입니다. 

이 단백질이 사실 광활한 바다를 자유롭게 유영하는 해파리로부터 비롯되었다는 사실을 알고 계시나요?

이번 활동에서는 NCBI Nucleotide에서 발광해파리 *Aequorea victoria*의 mature mRNA Green Fluorescent Protein(GFP) 서열을 검색하고, 이를 FASTA 형식으로 다운로드했습니다. 동일 데이터베이스에서 `Aequorea victoria GFP` 또는 accession code인 `M62654.1`을 입력하여, 다운로드 설정을 `Complete record`로 선택하시면 동일한 데이터를 다운로드할 수 있습니다. 또는 이번 주차의 폴더에 업로드해뒀으니, 그 파일을 활용하셔도 좋습니다.

그렇다면 다운로드한 GFP FASTA 파일을 이용한 자세한 실습 과정은 pdf와 ipynb 파일을 참고해주시길 바랍니다.