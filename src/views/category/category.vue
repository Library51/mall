<template>
  <div class="wrapper">
     <ul class="content">
    <li>lla1</li>
    <li>lla2</li>
    <li>lla3</li>
    <li>lla4</li>
    <li>lla5</li>
    <li>lla6</li>
    <li>lla7</li>
    <li>lla8</li>
    <li>lla9</li>
    <li>lla10</li>
    <li>lla11</li>
    <li>lla12</li>
    <li>lla13</li>
    <li>lla14</li>
    <li>lla15</li>
    <li>lla16</li>
    <li>lla17</li>
    <li>lla18</li>
    <li>lla19</li>
    <li>lla20</li>
    <li>lla21</li>
    <li>lla22</li>
    <li>lla23</li>
    <li>lla24</li>
    <li>lla25</li>
    <li>lla26</li>
    <li>lla27</li>
    <li>lla28</li>
    <li>lla29</li>
    <li>lla30</li>
    <li>lla31</li>
    <li>lla32</li>
    <li>lla33</li>
    <li>lla34</li>
    <li>lla35</li>
    <li>lla36</li>
    <li>lla37</li>
    <li>lla38</li>
    <li>lla39</li>
    <li>lla40</li>
    <li>lla41</li>
    <li>lla42</li>
    <li>lla43</li>
    <li>lla44</li>
    <li>lla45</li>
    <li>lla46</li>
    <li>lla47</li>
    <li>lla48</li>
    <li>lla49</li>
    <li>lla50</li>
    <li>lla51</li>
    <li>lla52</li>
    <li>lla53</li>
    <li>lla54</li>
    <li>lla55</li>
    <li>lla56</li>
    <li>lla57</li>
    <li>lla58</li>
    <li>lla59</li>
    <li>lla60</li>
    <li>lla61</li>
    <li>lla62</li>
    <li>lla63</li>
    <li>lla64</li>
    <li>lla65</li>
    <li>lla66</li>
    <li>lla67</li>
    <li>lla68</li>
    <li>lla69</li>
    <li>lla70</li>
    <li>lla71</li>
    <li>lla72</li>
    <li>lla73</li>
    <li>lla74</li>
    <li>lla75</li>
    <li>lla76</li>
    <li>lla77</li>
    <li>lla78</li>
    <li>lla79</li>
    <li>lla80</li>
    <li>lla81</li>
    <li>lla82</li>
    <li>lla83</li>
    <li>lla84</li>
    <li>lla85</li>
    <li>lla86</li>
    <li>lla87</li>
    <li>lla88</li>
    <li>lla89</li>
    <li>lla90</li>
    <li>lla91</li>
    <li>lla92</li>
    <li>lla93</li>
    <li>lla94</li>
    <li>lla95</li>
    <li>lla96</li>
    <li>lla97</li>
    <li>lla98</li>
    <li>lla99</li>
    <li>lla100</li>
  </ul calc>
  </div>
</template>

<script>
  import BScroll from 'better-scroll'
    export default {
        name: "category",
        data(){
           return{
             scroll : null
           }
      },
        created() {
          },
        mounted() {
          this.scroll = new BScroll(document.querySelector('.wrapper'),{
            probeType: 3,
            pullUpLoad:true
          })
          // this.scroll.on('scroll',(position)=>{
          //   console.log(position);
          // })
          this.scroll.on('pullingUp',()=>{
            console.log('ok');
          })
        }
    }

</script>

<style scoped>
  .wrapper{
    height: 150px;
    background-color: red;
    overflow: hidden;
  }

</style>
