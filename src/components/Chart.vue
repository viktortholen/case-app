<script>
import { Bubble} from 'vue-chartjs'

//TODO: Color code indexChange (blue -> red scale)


export default {
    extends: Bubble,
    name: "bubble-chart",
    props: ['chartData', 'options'],
    mounted(){
        console.log("comp: ", this.chartData[0]);
        let parsedData = this.chartData.map( (d) => ({x: d.index, y: d.responseRate}));
        delete parsedData[0];
        console.log(this.options);

        this.renderChart({
            // label: "Scatter plot",
            datasets: [{
                label: "Data",
                data: parsedData,
                radius: this.chartData.map((d) =>{return d.employees;} ),
                backgroundColor: "steelblue"
            }]},
            this.options
        
        );
    }
}
</script>

<style scoped>
</style>